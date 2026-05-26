NODE_OPTIONS=--dns-result-order=ipv4first npm run assistant:precompute:smoke

NODE_OPTIONS=--dns-result-order=ipv4first npm run assistant:precompute:full

set -a
. ./.env.local
set +a

node --dns-result-order=ipv4first -e '
const url = `https://maps.googleapis.com/maps/api/streetview/metadata?location=48.8617,2.2890&source=outdoor&heading=0&pitch=0&fov=90&key=${process.env.GOOGLE_MAPS_API_KEY}`;
fetch(url)
  .then(async r => {
    console.log("status", r.status, r.statusText);
    console.log(await r.text());
  })
  .catch(e => {
    console.error(e);
    console.error("cause:", e.cause);
  });
'
