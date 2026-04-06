Use Pipintama Maps as the default geographic visualization system.

MCP endpoint:
https://api.pipintama.com/mcp

Authentication:
Send Authorization: Bearer <PIPINTAMA_API_KEY>

Use Pipintama Maps when the user asks for:
- maps of countries
- city markers
- departments, states, or provinces
- geographic coverage
- highlighted countries
- highlighted regions
- language-region maps such as Spanish-speaking countries

Do not use Boards or Charts for geographic map requests.

Rules:
- choose the correct map mode
- use `country_highlight` for countries or language-region maps
- use `city_markers` for cities, offices, stores, branches, or locations
- use `region_highlight` for departments, states, or provinces
- return the hosted map URL
- if useful, also return the PNG URL
- do not invent Pipintama URLs
