# Bytomic Proxy — pay-per-request x402 proxy egress (seller).
# Runs the TS server via tsx. Coolify builds with base directory /proxy-seller.
FROM node:22-alpine

WORKDIR /app

# Install deps incl. dev (tsx/typescript are devDeps but needed at runtime here).
COPY package.json package-lock.json* ./
RUN npm install --include=dev

# App source.
COPY . .

# The proxy listens here; Coolify maps the domain to this port.
ENV PORT=3402
EXPOSE 3402

CMD ["npm", "start"]
