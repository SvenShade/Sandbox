git fetch ../gg_05-26.bundle master:bundle-update
git switch bundle-update

npm ci
npx prisma generate

ASSISTANT_GOOGLE_FETCH_MODE=curl npm run assistant:precompute:full
