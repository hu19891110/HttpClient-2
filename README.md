HttpClient is a client class for the HTTP protocol. It can be used to interact with another web server from within a PHP script. As well as retrieving information from a server, HttpClient can interact with a server via POST or GET. It can therefore be used as part of any script that needs to communicate with an application running on another site.

Grabbing an HTML page (static method)

$pageContents = HttpClient::quickGet('http://example.com/');

Posting a form and grabbing the response (static method)

$pageContents = HttpClient::quickPost('http://example.com/someForm', array(
    'name' => 'Some Name',
    'email' => 'email@example.com'
));

The static methods are easy to use, but seriously limit the functionality of the class as you cannot access returned headers or use facilities such as cookies or authentication.

A simple GET request using the class

$client = new HttpClient('http://example.com/');
if (!$client->get()) {
    die('An error occurred: '.$client->getError());
}
$pageContents = $client->getContent();

Check to see if a page exists

$client = new HttpClient('http://example.com/');
if (!$client->get()) {
    die('An error occurred: '.$client->getError());
}
if ($client->getStatus() == '404') {
    echo 'Page does not exist!';
}
$pageContents = $client->getContent();

Fake the User Agent string

$client = new HttpClient('http://example.com/');
$client->setUserAgent('Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.3a) Gecko/20021207');
if (!$client->get()) {
    die('An error occurred: '.$client->getError());
}
$pageContents = $client->getContent();

Print out the headers from a response

$client = new HttpClient('http://example.com/');
if (!$client->get()) {
    die('An error occurred: '.$client->getError());
}
print_r($client->getHeaders());

Print out the Cookies from a response

$client = new HttpClient('http://example.com/');
if (!$client->get()) {
    die('An error occurred: '.$client->getError());
}
print_r($client->getCookies());