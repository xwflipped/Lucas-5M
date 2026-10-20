# Lucas-5M AI Worker (personal, simulation only)

## What it does
Receives a manually selected UTC 5-minute target timestamp and two manually entered prediction-share prices. Worker fetches Binance BTCUSDT spot 5-minute candles and calls OpenAI, returning **UP / DOWN / WAIT** with reasons. Does **not** place orders, read account balances, or store OpenAI keys in GitHub Pages.

## Deployment checklist (Cloudflare dashboard or Wrangler)
1. Create a Worker using \`src/index.js\`, with compatibility date 2026-10-01.
2. Add encrypted Worker secrets **OPENAI_API_KEY** and **ACCESS_TOKEN** (long unique random string). Never commit either secret.
3. Create a Workers KV namespace and bind it as **RATE_KV**. A rate-limit check blocks the Worker if KV is absent. Note: KV read-modify-write is **not atomic**; for strong abuse protection add Cloudflare WAF rate limiting or a Durable Object, and set OpenAI project spend limits.
4. Set \`OPENAI_MODEL\` as optional environment variable (default gpt-4.1-mini). Verify availability and pricing in your OpenAI project.
5. Deploy and copy your HTTPS Worker URL into the Lucas-5M AI page. The frontend asks for your personal ACCESS_TOKEN and stores it in the iPad session only.
6. For real security, also protect Worker with Cloudflare Access or equivalent identity verification. Origin checks are **not** authentication; anyone with a stolen token can call the endpoint.
7. Only accept requests from the configured GitHub Pages origin. If the site origin changes, update ORIGIN and redeploy.

**Caveats**: Manually entered prices may be stale or non-executable. Binance spot candles may not match Binance prediction-market settlement index or start/end prices. GPT cannot infer reliable short-term probabilities from candles. No live trading, no auto-buying. iPad browser cannot guarantee a floating overlay on other apps.

**Cost**: OpenAI API billed separately from ChatGPT subscription. Set a small project budget and monitor usage.

**Important**: the Workers KV rate limiter is best-effort and non-atomic. For public or high-risk deployment use Cloudflare Access and atomic rate limits.