# CHAT2API

🤖 It's a simple ChatGPT TO API proxy.

🌟 You'll get free, unlimited access to GPT-3.5 without having to create an account.

💥 Supports AccessToken with an account, supports `O1-Preview/mini`, `GPT-4`, `GPT-4o/mini`, `GPTs`

🔍 The response format is exactly the same as the real API, and it's compatible with almost all clients.

👮 The matching user management terminal [Chat-Share] (https://github.com/h88782481/Chat-Share) needs to have the environment variables configured in advance (ENABLE_GATEWAY set to True and AUTO_SEED set to False) before use.


## Communication group

[https://t.me/chat2api] (https://t.me/chat2api)

Please read the repository documentation in its entirety, especially the FAQ section, before asking a question.

When asking a question, please include:

1. A screenshot of the startup log (encode sensitive information, including environment variables and version numbers)
2. The error reporting log information (encode sensitive information)
3. The status code and response body returned by the interface

## Sponsor

Thanks to Capsolver for sponsoring this project.For any human-machine verification codes on the market, you can use Capsolver to solve any problems you might have.

[![Capsolver](docs/capsolver.png)](https://www.capsolver.com/zh?utm_source=github&utm_medium=repo&utm_campaign=scraping&utm_term=chat2api)

## Function

The latest version number is stored in "version.txt."

### Reverse API functions
> - [x] Streaming and non-streaming transfer
Login-free GPT-3.5 dialogue
GPT-3.5 model dialogue (if the model name isn't passed in and doesn't contain gpt-4, gpt-3.5 is used by default, which is text-davinci-002-render-sha).
And finally, if you want to use GPT-4, you'll need to pass in the model name (like gpt-4, gpt-4o, gpt-4o-mini, or gpt-4-mobile) and an AccessToken.
And for the O1 series model, you'll need to pass in the model name to include o1-preview or o1-mini, and you'll also need an AccessToken.
Then there's GPT-4 model drawing, coding, and networking.
Support for GPTs is also available (pass in model name: gpt-4-gizmo-g-*)
Support for Team Plus accounts is also required (team account ID required).
You can also upload images and files (in formats compatible with the API, including URLs and base64).
It can be used as a gateway and deployed across multiple machines.
It can poll for multiple accounts, supporting both AccessToken and RefreshToken.
It can retry failed requests and automatically poll for the next token.
It's got token management, support for uploading and clearing tokens.
It'll refresh your AccessToken every few days with a RefreshToken, and you can choose to refresh it manually whenever you want, or have it refresh on its own every four days at 3:00 p.m.
We'll need to enable history to support file download.
[x] Allow for the preview of the O1-Preview/mini model's output from the inference process

Official website mirroring function
> - [x] Support native mirroring of the official website
The background account pool is randomly selected, and the "Seed" is set to a random account.
> - [x] Enter `RefreshToken` or `AccessToken` to log in directly
Support O1-Preview/mini, GPT-4, GPT-4o/mini.
And finally, we'll disable sensitive information interfaces and some setting interfaces.
- [x] /login login page, automatically jump to the login page after logging out
- [x] Use /?token=xxx to log in directly. xxx is `RefreshToken`, `AccessToken`, or `SeedToken` (random seed)


TODO:
- [ ] Mirroring support for GPTs
We don't have mirroring support for GPTs yet, but please raise an issue if you have any questions.

## Reverse API

It's fully OpenAI format API, supports passing in AccessToken or RefreshToken, and is available for GPT-4, GPT-4o, GPTs, O1-Preview, and O1-Mini.

[ ] We don't have mirroring support for GPTs yet, but if you need it, please raise an issue.
[ ] The reverse API is fully openAI format. You can use an AccessToken or a RefreshToken. It's available for GPT-4, GPT-4o, GPTs, and O1-Preview, and O1-Mini.
curl --location 'http://127.0.0.1:5005/v1/chat/completions'
--header 'Content-Type: application/json'
--header 'Authorization: Bearer ' .token .
--data '{
     "model": "gpt-3.5-turbo",
     "messages": [{"role": 'user', 'content': 'Say this is a test!'}],
     "stream": true
   )"
Then, add "stream": true.

Pass in your account's AccessToken or RefreshToken as Token.
You can also fill in the value of the environment variable "Authorization" that you set, and a background account will be selected at random.

If you have a team account, you can pass in the `ChatGPT-Account-ID` to use the team workspace.

Method 1:
Pass in the `ChatGPT-Account-ID` value in headers.

- Method 2:
`Authorization: Bearer <AccessToken or RefreshToken>,<ChatGPT-Account-ID>`

If the AUTHORIZATION environment variable is set, the set value can be passed in as "Token" for multi-token polling.

For AccessToken acquisition, after logging in to the chatgpt official website, open [https://chatgpt.com/api/auth/session] to obtain the value of AccessToken.
The method for acquiring a refresh token isn't included here.
Login-free gpt-3.5 doesn't require a Token.

## Tokens management

1. Set the environment variable `AUTHORIZATION` as the `authorization code` and then run the program.

2. Go to `/tokens` or `/{api_prefix}/tokens` to see the number of existing tokens, upload new tokens, or clear tokens.

3. Pass in the "authorization code" configured in "AUTHORIZATION" when requesting to use the polled tokens for conversation.

![tokens.png] (docs/tokens.png)

## Official website native image

First, set the environment variable ENABLE_GATEWAY to true and then run the program. Keep in mind that after it's enabled, others can also access your gateway directly through the domain name.

Next, upload the refresh token or access token on the tokens management page.

Then, visit the login page at "/login."

![login.png]

Then go to the native mirror page of the official website and use

![chatgpt.png]

## Environment variables

Each environment variable has a default value, so if you're not sure what it means, don't set it or pass an empty value. Also, strings don't need to be quoted.

[cat-] Category [var-] Variable name [ex-] Example value [val-] Default value [des-] Description [cat-]
4. Go to the native mirror page of the official website and use ![chatgpt.png] (docs/chatgpt.png)
## Environment Variables
Each environment variable has a default value. If you don't understand the meaning of the environment variable, don't set it and don't pass an empty value. Strings don't need to be quoted.
| Category | Variable name | Example value | Default value | Description |
|------|-----------------|----------------------------------|----------------------------------|----------------------------------|
[chatgpt.png] (docs/chatgpt.png)
## Environment variables
Each environment variable has a default value. If you don't understand the meaning of the environment variable, don't set it, and don't pass an empty value. Strings don't need to be quoted.
[category] [variable name] [example value] [default value] [description]
| Security-related | API_PREFIX | `your_prefix` | `None` | API prefix password. If not set, it's easy for others to access it. After setting, you need to request /your_prefix/v1/chat/completions.
Security-related stuff:
API_PREFIX: Set your API prefix password here. If you don't set one, it'll be easy for others to access it. After setting it, you'll need to request /your_prefix/v1/chat/completions.
AUTHORIZATION: Set your authorization codes for polling tokens using multiple accounts. Separate them with commas.
Here's the authorization key: `your_auth_key`. If you're using private gateways, you'll need to set the auth_key request header to set this item.
Here are some request-related settings:
-	CHATGPT_BASE_URL: https://chatgpt.com
-	AUTH_KEY: your_auth_key

The CHATGPT_BASE_URL setting changes the requested website. Multiple gateways separated by commas are supported.
Here's what you need to know about the Auth Key request header:
-	It's set to "None" by default.
-	If you're using private gateways, you'll need to set this to your Auth Key.
-	The request-related setting is set to "CHATGPT_BASE_URL" by default.
-	It's set to "https://chatgpt.com" here.
-	If you want to change the website that's requested, you can set the setting to multiple gateways separated by commas.
-	If you want to enable a global proxy URL, set the setting to "PROXY_URL" and enter "http://ip:port" or "http://username:password@ip:port".
-	If you want to use multiple proxies, set the setting to "PROXY_URL" and enter "[]" here.
Here's what you need to know about the EXPORT_PROXY_URL: it's set to `http://ip:port` or `http://username:password@ip:port` by default. If you want to prevent the origin server IP address from being leaked when requesting images and files, set it to `None`.
Function-related: HISTORY_DISABLED = true; return the conversation ID and don't save chat history.
Here are some more details on the export proxy URL: it can be set to either "http://ip:port" or "http://username:password@ip:port" and it's set to "None" by default. This is to prevent the origin server IP address from being leaked when images and files are requested.
There's also a function-related setting called HISTORY_DISABLED, which is set to "true" by default. This means that chat history won't be saved and the conversation ID will be returned.
The difficulty of the proof of work to be solved is set to "00003a" by default. If you don't understand this, don't set it.
Function-related: HISTORY_DISABLED: Whether to disable chat history and return the conversation ID. POW_DIFFICULTY: The difficulty of the proof of work to be solved. Set to 00003a by default. RETRY_TIMES: The number of retries in case of an error. Using AUTHORIZATION will automatically randomize/poll the next account.
| CONVERSATION_ONLY | `false` | `false` | Whether to use the conversation interface directly. If the gateway you're using supports automatic POW resolution, enable it.
You can set the retry times to 3 and the conversation-only setting to false. This will let you use the conversation interface directly. If your gateway supports automatic POW resolution, enable it. Also, enable the ENABLE_LIMIT setting to true. This will prevent you from exceeding the official limit of times and will help prevent a ban.
| UPLOAD_BY_URL | `false` | `false` | Whether to use the conversation interface directly. If the gateway you're using supports automatic POW resolution, enable it. | ENABLE_LIMIT | `true` | `true` | After being enabled, it won't try to exceed the official limit of times and will prevent being banned as much as possible. | UPLOAD_BY_URL | `false` | `false` | After being enabled, the conversation will be carried out according to URL+space+body. The content of the URL will be parsed automatically and uploaded, and multiple URLs will be separated by spaces.
| SCHEDULED_REFRESH | `false` | `false` | Whether to refresh the Access Token regularly. If enabled, the Access Token will be refreshed once every time the program is started and once every four days at 3:00 p.m.
The RANDOM_TOKEN setting determines whether to randomly select the background token. When this setting is enabled, the background account is randomly selected. When disabled, the polling is in order.
Gateway function: ENABLE_GATEWAY: Whether to enable gateway mode. If it's turned on, you can use the mirror site, but it won't be protected.
| AUTO_SEED: Whether to enable random account mode. It's enabled by default. After entering a seed, the background token is randomly matched. After it's turned off, you need to manually connect to the interface to control the token.

| ENABLE_GATEWAY: Whether to enable gateway mode. After it's turned on, you can use the mirror site, but it won't be protected.

| AUTO_SEED: Whether to enable random account mode. It's enabled by default. After entering a seed, the background token is randomly matched. After it's turned off, you need to manually connect to the interface to control the token.

## Deployment

### Zeabur deployment

[![Deploy on Zeabur: https://zeabur.com/button.svg]() https://zeabur.com/templates/6HEGIZ?referralCode=LanQian528

### Direct deployment

Then just run this command: bash
git clone https://github.com/LanQian528/chat2api
cd chat2api
pip install -r requirements.txt
Then, run "python app.py"
Then, you can cd to chat2api and run pip install -r requirements.txt python app.py.

### Docker deployment

You'll need to install Docker and Docker Compose.

Then, you'll need to install Docker and Docker Compose.
docker run -d
  --name chat2api
  -p 5005:5005
  lanqian528/chat2api:latest
Then, you can use the following command:

### (Recommended, available with PLUS account) Docker Compose deployment

Create a new directory, for example chat2api, and go to that directory:

Then, you'll need to run the following command:
mkdir chat2api
cd chat2api
Then, go to the chat2api directory and run the following command:

Then, download the docker-compose.yml file from the repository in this directory:

Then, you can run the following command:
Then, get this file: https://raw.githubusercontent.com/LanQian528/chat2api/main/docker-compose-warp.yml
Then, modify the environment variables in the docker-compose-warp.yml file and save it.

Modify the environment variables in the docker-compose-warp.yml file, and save it.

Then, save the file as docker-compose-warp.yml.
docker-compose up -d
Then, save the file as docker-compose-warp.yml.


## Frequently Asked Questions

> - Error codes:
- `401`: The current IP address doesn't support log-in-free access. Try again using a different IP address, or set a proxy in the environment variable `PROXY_URL`. Otherwise, your authentication may have failed.
If you see a `403` error, check the log for more details.
If you see a code of 429, it means the current IP has tried to access more than the limit within the last hour. You can try again later or change the IP.
If you see a 500 error, that means there's been an internal server error and the request failed.
If you see a 502 error, that means the server gateway is having problems or the network is down. In that case, try switching networks.

Here are some known issues:
Many Japanese IPs don't support free login, and GPT-3.5 recommends using a US IP for free login.
99% of accounts support free "GPT-4o," but it's enabled based on the IP region, and right now, Japanese and Singaporean IPs are known to have a higher probability of being enabled.

And finally, what's the deal with the environment variable AUTHORIZATION?
It's an authentication set by chat2api itself, and after setting it, you can use the saved tokens to poll and pass it as APIKEY during the request.
And how do I get the AccessToken?
After logging in to the chatgpt website, open [https://chatgpt.com/api/auth/session] to get the value of `accessToken`.


## License

MIT License
