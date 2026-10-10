# Cigo Aircare & Carsafe MCP Connector

Connect MCP-compatible clients to Cigo's hosted MCP server for vehicle cabin-filter matching,
HVAC product specifications and B2B inquiries. No local Python server or API key
is required. An internet connection and a client with remote MCP support are needed.

## Tools

| Tool | Purpose | Writes data |
| --- | --- | --- |
| `search_carsafe` | Find Carsafe products by vehicle model and year; return product purchase links. | No |
| `get_hvac_filter_info` | Read FFU/BFU dimensions, filtration performance, BFU pressure loss and airflow-specific power comparisons. | No |
| `check_environment` | Query regional weather/air-quality information and filter-care guidance. | No |
| `set_crm_lifecycle` | Save vehicle/driving information with a hashed user identifier and a suggested replacement date. | Yes |
| `submit_b2b_inquiry` | Submit company/contact information and an inquiry to Cigo. | Yes |

## Connect

After installing the plugin, enable the `cigo-aircare` MCP server in Cursor.
For direct setup before marketplace approval, add the following entry to your
Cursor MCP settings (`mcp.json`):

```json
{
  "mcpServers": {
    "cigo-aircare": {
      "url": "https://cigo-mcp-system-wzoy.onrender.com/mcp/"
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
Cigo's configured Supabase inquiry store. `set_crm_lifecycle` stores a hashed
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


