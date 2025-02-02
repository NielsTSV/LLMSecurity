# Setup
1. create + enter venv
    - `python -m venv venv`
    - `source myvenv/bin/activate`
2. pip install requirements
    - `pip install -r requirements.txt`


# Garak
Security Tool acquired by Nvidia AI
- https://github.com/NVIDIA/garak
- https://docs.garak.ai/
- https://reference.garak.ai/

### Local Model (REST)
- create a .json with the model specifications and api call
    - see claude_config.json for example (or https://reference.garak.ai/en/latest/garak.generators.rest.html + https://docs.anthropic.com/en/api/messages)
    - or follow this video: https://www.youtube.com/watch?v=f713_sFqItY&ab_channel=EmbraceTheRed
    - set env variable: `REST_API_KEY=`
- Run tests
    - List all tests: `garak --list_probes`
    - Run specific test: `garak --model_type rest -G claude-config.json --probes malwaregen.Evasion --generations 2`
    - Run all tests: `garak evaluate --config claude_config.yaml`
- Report
    - By default logs are stored under ~/.local/share/garak/






### Create Json from API Call (https://docs.anthropic.com/en/api/messages)
Api Call:
```
curl https://api.anthropic.com/v1/messages \
     --header "x-api-key: $REST_API_KEY" \
     --header "anthropic-version: 2023-06-01" \
     --header "content-type: application/json" \
     --data \
'{
    "model": "claude-3-5-haiku-latest",
    "max_tokens": 1024,
    "messages": [
        {"role": "user", "content": "Hello, world"}
    ]
}'
```
to
```
{
    "rest": {
       "RestGenerator": {
          "name": "claude-tester",
          "uri": "https://api.anthropic.com/v1/messages",
          "method": "post",
          "headers": {
             "x-api-key": "$KEY",
             "anthropic-version": "2023-06-01",
             "content-type": "application/json"
          },
          "req_template_json_object": {
            "model": "claude-3-5-sonnet-20241022",
            "max_tokens": 1024,
            "messages": [
                {"role": "user", "content": "$INPUT"}
            ]
          },
          "response_json": true,
          "response_json_field": "$.content[0].text"
       }
    }
 }
```

