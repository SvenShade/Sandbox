node -e "const fs=require('fs'); const m=fs.readFileSync('.env.local','utf8').match(/^GOOGLE_MAPS_API_KEY=(.*)$/m); console.log(m ? 'GOOGLE_MAPS_API_KEY is set, length=' + m[1].length : 'GOOGLE_MAPS_API_KEY missing')"

set -a
. ./.env.local
set +a

curl -sS "https://maps.googleapis.com/maps/api/streetview/metadata?location=48.8617,2.2890&source=outdoor&heading=0&pitch=0&fov=90&key=${GOOGLE_MAPS_API_KEY}"

curl -4 -sS "https://maps.googleapis.com/maps/api/streetview/metadata?location=48.8617,2.2890&source=outdoor&heading=0&pitch=0&fov=90&key=${GOOGLE_MAPS_API_KEY}"

NODE_OPTIONS=--dns-result-order=ipv4first npm run assistant:precompute:smoke
