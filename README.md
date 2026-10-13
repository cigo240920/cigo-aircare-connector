# Cigo Aircare & Carsafe MCP Connector



Connect MCP-compatible clients to Cigo's hosted MCP server for vehicle cabin-filter matching,

HVAC product specifications and B2B inquiries. No local Python server or API key

is required. An internet connection and a client with remote MCP support are needed.



## Quick start / 쉽게 연결하기



No server installation or API key is needed. Your AI app must support remote MCP; its own plan and usage limits still apply.



**Cursor:** [Add Cigo MCP to Cursor](https://cursor.com/link/mcp/install?name=cigo-aircare&config=eyJ1cmwiOiJodHRwczovL2NpZ28tbWNwLXN5c3RlbS13em95Lm9ucmVuZGVyLmNvbS9tY3AvP3NvdXJjZT1jdXJzb3IifQ%3D%3D), then review and confirm the connection in Cursor.



**Manus:** Settings → Connectors → Create → Custom MCP. Enter the name **Cigo Aircare & Carsafe**, choose HTTP, and use the server URL below. No custom authorization header is needed. Save the connector. Creation was verified with a free Manus account on 2026-10-13; this does not publish it to all Manus users.



**한국어 안내:** Cursor는 위 설치 링크를 누른 뒤 연결을 확인하세요. Manus는 설정 → 커넥터 → 생성 → 사용자 정의 MCP에서 아래 주소를 입력하고 저장하세요. 별도 서버 설치나 API 키는 필요 없습니다.



Manus server URL: https://cigo-mcp-system-wzoy.onrender.com/mcp/?source=manus



Try asking: "씨고 BFU 필터의 규격과 풍량별 소비전력을 알려줘." / "Find the cabin filter for my vehicle model and year."



## Gemini CLI



Install this connector from the public repository:



```sh

gemini extensions install https://github.com/cigo240920/cigo-aircare-connector

```



Review the extension permissions, restart Gemini CLI, then use `/mcp` to check the connection. No Cigo API key is needed. This extension is for Gemini CLI, not the Gemini consumer app.



To get later connector changes, run `gemini extensions update cigo-aircare`. The hosted server is managed separately.



## Tools



| Tool | Purpose | Writes data |

| --- | --- | --- |

| `search_carsafe` | Find Carsafe products by vehicle model and year; return product purchase links. | No inquiry; product usage is logged |

| `get_hvac_filter_info` | Read FFU/BFU dimensions, filtration performance, BFU pressure loss and airflow-specific power comparisons. | No inquiry; product usage is logged |

| `check_environment` | Query regional weather/air-quality information and filter-care guidance. | No |

| `set_crm_lifecycle` | Save vehicle/driving information with a hashed user identifier and a suggested replacement date. | Yes |

| `submit_b2b_inquiry` | Submit company/contact information and an inquiry to Cigo. | Yes |



## Connect



For manual setup, add the following entry to your Cursor MCP settings (`mcp.json`):



```json

{

  "mcpServers": {

    "cigo-aircare": {

      "url": "https://cigo-mcp-system-wzoy.onrender.com/mcp/?source=cursor"

    }

  }

}

```



This package contains only connection configuration and documentation. It has no

shell commands, installation scripts or hooks. The hosted server currently does

not require authentication. Restart the connection if Cursor caches an older tool list.



## Example requests



- "2020년식 쏘렌토에 맞는 카세이프 필터를 찾아줘."

- "씨고 FFU와 BFU 필터의 규격과 소비전력을 비교해줘."

- "BFU의 풍량 17 CMM 조건에서 소비전력 절감률을 알려줘."

- "Draft a B2B inquiry for BFU filters; show me the details before submitting."



Product lookup does not submit an inquiry or place an order. Follow purchase links

to the external store for checkout. Quotes, supply availability and delivery terms

need separate confirmation from Cigo. A CRM record is not evidence that an email

or SMS reminder has been sent.



## Data handling



Tool arguments are sent over HTTPS to Cigo's hosted server on Render. Do not enter

passwords, payment information or unrelated personal information into tool fields.

Lookup tools need only the relevant vehicle, filter type or region.



When requested by the user, `submit_b2b_inquiry` sends the supplied company,

contact details, destination country, language, subject and inquiry details to

Cigo's configured Supabase inquiry store. Foreign-language inquiry subjects and details are sent to Microsoft Azure Translator for Korean machine translation after the original is saved. Translation failure does not discard the original. `set_crm_lifecycle` stores a hashed

identifier, vehicle/driving details and replacement date on the server. Hashing

an identifier does not make the entire record anonymous.



Before a write action, show the information to be sent and obtain the user's

confirmation. Report successful submission only after a successful server result.

For data handling, retention or deletion questions, contact **cigo240920@gmail.com**.



## Measurement limits



Preserve the tool's measurement conditions. Dimension units are unconfirmed.

The 0.3 micrometre efficiency condition comes from the brochure; do not attribute

it to the separate BFU test figures. Compare power consumption only at the listed

airflows; do not promise site-specific electricity-bill savings or infer certifications.



## Support



Email: **cigo240920@gmail.com**



Source: https://github.com/cigo240920/cigo-aircare-connector



Registry name: `io.github.cigo240920/cigo-aircare`



## License scope



The MIT license in this directory covers only the connection configuration and

documentation in this connector repository. It does not grant a license to the

repository's server implementation, product data, source documents or trademarks.






## Channel attribution and product analytics

Cigo records the connection URL's channel label, lookup tool, returned product codes, and time in its private Supabase store. It does not put raw search text, conversation transcripts, IP addresses, or contact details in the usage table. Inquiry details remain in the existing private inquiry store.

Lookup results include an optional signed `journey_token`. Pass it to subsequent product lookups and the confirmed B2B inquiry in the same customer conversation to link that journey; never reuse it for another customer. Tokens expire after 24 hours. Without a valid token, earlier lookups are not linked. Channel labels are not verified identities or proof of the site where a person first discovered Cigo. Unknown channels remain unknown. No purchase-completion tracking is included.

Use the relevant connection address for new installations:

| Connection | MCP URL |
| --- | --- |
| Cursor | https://cigo-mcp-system-wzoy.onrender.com/mcp/?source=cursor |
| Manus | https://cigo-mcp-system-wzoy.onrender.com/mcp/?source=manus |
| Gemini CLI | https://cigo-mcp-system-wzoy.onrender.com/mcp/?source=gemini |
| This GitHub guide / other clients | https://cigo-mcp-system-wzoy.onrender.com/mcp/?source=github |

Existing untagged URLs still work. Reconnect after changing a URL to refresh tool descriptions. Analytics failures do not block lookups or inquiry submission.
