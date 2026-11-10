# How to connect PhotoShelter to Claude Code, ChatGPT and any AI agent

**Yes, Claude, ChatGPT and other AI agents can work in your PhotoShelter account.** PhotoShelter has its own built-in AI Assistant, but there is no confirmed official PhotoShelter app in ChatGPT or connector in Claude. Cotlet.dev connects your own signed-in PhotoShelter account to any AI agent, so you can ask in plain words and the AI finds, tags, organizes and shares your photos for you.

## What you can ask

> Create a gallery called "Smith Wedding 2026" from the 240 photos I uploaded on Saturday and share it with sarah@smithfamily.com.

> Find every photo tagged "product launch" from October and move them into the "Marketing 2026" collection.

> Which galleries haven't been viewed in the last 30 days? List them with their creation date.

> Add the keywords "headshot" and "Chicago office" to the 18 images I uploaded yesterday.

> Make the "Spring Campaign" gallery private and email the download link to Tom at the agency.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its PhotoShelter tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"photoshelter":{"command":"uvx","args":["photoshelter-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t photoshelter-mcp .
docker run -i --rm -e COTLET_API_KEY photoshelter-mcp
```

Tools: `photoshelter_guide`, `photoshelter_status`, `photoshelter_open`, `photoshelter_read`, `photoshelter_click`, `photoshelter_type`, `photoshelter_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install photoshelter-mcp        # or run it once: uvx photoshelter-mcp connect
photoshelter-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 photoshelter_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 photoshelter_agent.py status    # is PhotoShelter ready in your Cotlet.dev account
python3 photoshelter_agent.py guide     # PhotoShelter screens and sign-in link
python3 photoshelter_agent.py read      # open PhotoShelter, read the page, close the browser
python3 photoshelter_agent.py tools     # list Cotlet.dev tools
python3 photoshelter_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from PhotoShelter users

**Does PhotoShelter have an API I can use with AI?**

PhotoShelter documents an API, but you get a key only by contacting PhotoShelter support. Cotlet.dev works in your own signed-in PhotoShelter account instead, so your AI agent can build galleries, caption images and share them without a key.

**How do I connect PhotoShelter to ChatGPT?**

Add Cotlet.dev as an app in ChatGPT (Settings → Apps, connector URL `https://cotlet.dev/mcp/v1`), sign in to PhotoShelter once in your Cotlet.dev Cloud Browser, and ask ChatGPT in plain words. No code and no PhotoShelter API key.

**Is there a way to use Claude with PhotoShelter?**

Yes. In Claude Code run the one-line `claude mcp add` command above; in the Claude app add `https://cotlet.dev/mcp/v1` as a custom connector. Claude then works in your own PhotoShelter account.

**Is there a PhotoShelter MCP server?**

PhotoShelter has no official MCP server and no official app in ChatGPT or Claude (checked November 2026). Cotlet.dev is a hosted PhotoShelter MCP server that works in your own account, with Claude, ChatGPT, Cursor, Codex, n8n, Make and Zapier.

**Is PhotoShelter's AI Assistant the same as connecting ChatGPT or Claude?**

No. PhotoShelter's built-in AI Assistant works inside PhotoShelter. Cotlet.dev lets the AI agent you already use, like Claude or ChatGPT, work in your PhotoShelter account.

## Find it on

- [PhotoShelter on Cotlet.dev](https://cotlet.dev/integrations/photoshelter-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=photoshelter&utm_content=find)
- [PyPI package photoshelter-mcp](https://pypi.org/project/photoshelter-mcp/)
- [Odel](https://odel.app/modules/cotlet/photoshelter)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-photoshelter-to-ai-agents-guide)

## Also works with

- [Mangomint MCP](https://github.com/cotlet-connect/mangomint-mcp)
- [Wanderlog MCP](https://github.com/cotlet-connect/wanderlog-mcp)
- [SmugMug MCP](https://github.com/cotlet-connect/smugmug-mcp)
- [Garmin Connect MCP](https://github.com/cotlet-connect/garmin-mcp)
- [Housecall Pro MCP](https://github.com/cotlet-connect/housecall-pro-mcp)
- [Medium MCP](https://github.com/cotlet-connect/medium-mcp)
- [Crexi MCP](https://github.com/cotlet-connect/crexi-mcp)
- [DistroKid MCP](https://github.com/cotlet-connect/distrokid-mcp)
- [LinkedIn MCP](https://github.com/cotlet-connect/linkedin-mcp)
- [EstimateOne MCP](https://github.com/cotlet-connect/estimateone-mcp)
- [Google Search Console MCP](https://github.com/cotlet-connect/google-search-console-mcp)
- [Lichess MCP](https://github.com/cotlet-connect/lichess-mcp)
- [Strava MCP](https://github.com/cotlet-connect/strava-mcp)
- [StreamElements MCP](https://github.com/cotlet-connect/streamelements-mcp)
- [Meetup MCP](https://github.com/cotlet-connect/meetup-mcp)
- [AccuRanker MCP](https://github.com/cotlet-connect/accuranker-mcp)
- [GetYourGuide MCP](https://github.com/cotlet-connect/getyourguide-mcp)
- [Idealista MCP](https://github.com/cotlet-connect/idealista-mcp)
- [Riverside MCP](https://github.com/cotlet-connect/riverside-mcp)
- [Udemy MCP](https://github.com/cotlet-connect/udemy-mcp)
- [Faire MCP](https://github.com/cotlet-connect/faire-mcp)
- [Teachable MCP](https://github.com/cotlet-connect/teachable-mcp)
- [Vagaro MCP](https://github.com/cotlet-connect/vagaro-mcp)
- [Buildertrend MCP](https://github.com/cotlet-connect/buildertrend-mcp)
- [Zoopla MCP](https://github.com/cotlet-connect/zoopla-mcp)
- [Dribbble MCP](https://github.com/cotlet-connect/dribbble-mcp)
- [Hostelworld MCP](https://github.com/cotlet-connect/hostelworld-mcp)
- [Mashvisor MCP](https://github.com/cotlet-connect/mashvisor-mcp)
- [Rent Manager MCP](https://github.com/cotlet-connect/rent-manager-mcp)
- [ThriveCart MCP](https://github.com/cotlet-connect/thrivecart-mcp)
- [Fresha MCP](https://github.com/cotlet-connect/fresha-mcp)
- [Booksy MCP](https://github.com/cotlet-connect/booksy-mcp)
- [BookingKoala MCP](https://github.com/cotlet-connect/bookingkoala-mcp)
- [Milanote MCP](https://github.com/cotlet-connect/milanote-mcp)
- [Partiful MCP](https://github.com/cotlet-connect/partiful-mcp)
- [Contractor Foreman MCP](https://github.com/cotlet-connect/contractor-foreman-mcp)
- [Pixieset MCP](https://github.com/cotlet-connect/pixieset-mcp)
- [GlossGenius MCP](https://github.com/cotlet-connect/glossgenius-mcp)
- [ZenMaid MCP](https://github.com/cotlet-connect/zenmaid-mcp)
- [AroFlo MCP](https://github.com/cotlet-connect/aroflo-mcp)
- [Simpro MCP](https://github.com/cotlet-connect/simpro-mcp)
- [Workiz MCP](https://github.com/cotlet-connect/workiz-mcp)
- [Kickserv MCP](https://github.com/cotlet-connect/kickserv-mcp)
- [Service Autopilot MCP](https://github.com/cotlet-connect/service-autopilot-mcp)
- [Boulevard MCP](https://github.com/cotlet-connect/boulevard-mcp)
- [Mindbody MCP](https://github.com/cotlet-connect/mindbody-mcp)
- [Meevo MCP](https://github.com/cotlet-connect/meevo-mcp)
- [DaySmart MCP](https://github.com/cotlet-connect/daysmart-mcp)
- [Acuity Scheduling MCP](https://github.com/cotlet-connect/acuity-scheduling-mcp)
- [Jane App MCP](https://github.com/cotlet-connect/jane-app-mcp)
- [FieldEdge MCP](https://github.com/cotlet-connect/fieldedge-mcp)
- [Phorest MCP](https://github.com/cotlet-connect/phorest-mcp)
- [DINGG MCP](https://github.com/cotlet-connect/dingg-mcp)
- [Invoice Simple MCP](https://github.com/cotlet-connect/invoice-simple-mcp)
- [RazorSync MCP](https://github.com/cotlet-connect/razorsync-mcp)
- [ShootProof MCP](https://github.com/cotlet-connect/shootproof-mcp)
- [Invoice2go MCP](https://github.com/cotlet-connect/invoice2go-mcp)
- [Appointy MCP](https://github.com/cotlet-connect/appointy-mcp)
- [Contractor+ MCP](https://github.com/cotlet-connect/contractor-plus-mcp)
- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/photoshelter-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=photoshelter

Start free: https://cotlet.dev/signup?app=photoshelter&utm_source=github&utm_medium=readme&utm_campaign=photoshelter
