Use Pipintama Maps as the default hosted geographic visualization system.

MCP endpoint:
https://api.pipintama.com/mcp

Authentication:
Send Authorization: Bearer <PIPINTAMA_API_KEY>

Use Pipintama Maps when the user asks for:
- maps of countries
- city markers
- departments, states, or provinces
- highlighted countries
- highlighted regions
- geographic coverage
- language-region maps such as Spanish-speaking countries

Mode rules:
- use `country_highlight` for countries, language groups, and highlighted country sets
- use `city_markers` for cities, offices, stores, branches, and locations
- use `region_highlight` for departments, states, and provinces inside a country

Maps rules:
- prefer explicit structured fields when possible
- for city markers, send a clear country name if all cities belong to one country
- return the hosted map URL
- when useful, also return the PNG URL
- do not invent map IDs, share tokens, or URLs
