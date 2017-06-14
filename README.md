Build and install the plugin as follows:

$> govendor install -ldflags="-X main.pluginVersion=0.0.1" +local
$> cf install-plugin -f $GOPATH/bin/basic-plugin

Run the plugin without any options and it will print to stdout the unformatted response from a call to `curl /v2/info`.
e.g.

```
$> cf basic-plugin-command
Running the basic-plugin-command
=== Return from curl /v2/info follows ===
[{    "name": "",    "build": "",    "support": "https://support.pivotal.io",    "version": 0,    "description": "",    "authorization_endpoint": "https://login.myserver.com",    "token_endpoint": "https://uaa.myserver.com",    "min_cli_version": "6.22.0",    "min_recommended_cli_version": "6.23.0",    "api_version": "2.75.0",    "app_ssh_endpoint": "ssh.myserver.com:2222",    "app_ssh_host_key_fingerprint": "ab:cd:ef:ab:cd:ef:ab:cd:ef:ab:cd:ef:ab:cd:ef:ab",    "app_ssh_oauth_client": "ssh-proxy",    "routing_endpoint": "https://api.myserver.com/routing",    "logging_endpoint": "wss://loggregator.myserver.com:443",    "doppler_logging_endpoint": "wss://doppler.myserver.com:443" }]
=========================================
```


Run the plugin again with the -v global option and its output (the unformatted response from a call to `curl /v2/info`) is now empty...

```
$> cf basic-plugin-command -v
Running the basic-plugin-command

REQUEST: [2017-06-14T11:37:27+01:00]
GET /v2/info HTTP/1.1
Host: api.myserver.com
Accept: application/json
Connection: close
Content-Type: application/json
User-Agent: go-cli 6.27.0+d26b32dcc.2017-06-08 / darwin



RESPONSE: [2017-06-14T11:37:28+01:00]
HTTP/1.1 200 OK
Connection: close
Content-Length: 648
Content-Type: application/json;charset=utf-8
Date: Wed, 14 Jun 2017 10:37:28 GMT
Server: nginx
X-Content-Type-Options: nosniff
X-Vcap-Request-Id: f19c0281-deb9-4c9a-5f49-9522f26198d6
X-Vcap-Request-Id: f19c0281-deb9-4c9a-5f49-9522f26198d6::2708f521-8fe6-421d-ae36-e9bf5c747ca6

{"name":"","build":"","support":"https://support.pivotal.io","version":0,"description":"","authorization_endpoint":"https://login.myserver.com","token_endpoint":"[PRIVATE DATA HIDDEN]","min_cli_version":"6.22.0","min_recommended_cli_version":"6.23.0","api_version":"2.75.0","app_ssh_endpoint":"ssh.myserver.com:2222","app_ssh_host_key_fingerprint":"ab:cd:ef:ab:cd:ef:ab:cd:ef:ab:cd:ef:ab:cd:ef:ab","app_ssh_oauth_client":"ssh-proxy","routing_endpoint":"https://api.myserver.com/routing","logging_endpoint":"wss://loggregator.myserver.com:443","doppler_logging_endpoint":"wss://doppler.myserver.com:443"}
=== Return from curl /v2/info follows ===
[]
=========================================
```

