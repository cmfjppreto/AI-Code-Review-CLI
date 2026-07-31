# Troubleshooting

## TLS/SSL Error in On-Prem TFS

Prefer using a CA bundle:

```yaml
tfs:
  verify_ssl: true
  ca_bundle: C:/certs/corporate-root-ca.pem
```

Avoid `verify_ssl: false` except for temporary troubleshooting.

## Bedrock Example

**Option 1 — Bedrock long-term API key** (AWS Console → Amazon Bedrock → API Keys):
```yaml
llm:
  provider: bedrock
  model: arn:aws:bedrock:eu-north-1:123456789:application-inference-profile/xxxxxxxx

bedrock:
  region: eu-north-1
  access_key_id: ABSK...   # long-term API key — no secret_access_key
```

**Option 2 — IAM explicit credentials** (access key ID + secret):
```yaml
llm:
  provider: bedrock
  model: anthropic.claude-3-5-sonnet-20240620-v1:0

bedrock:
  region: us-east-1
  access_key_id: AKIA...
  secret_access_key: wJalr...
  # session_token: ...   # optional, for temporary STS credentials
```

**Option 3 — AWS SSO / named profile**:
```yaml
bedrock:
  region: us-east-1
  profile: my-sso-profile
```