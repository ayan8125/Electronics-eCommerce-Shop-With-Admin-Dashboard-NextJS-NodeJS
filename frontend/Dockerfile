# ------------------------
# 1. Build Stage
# ------------------------
FROM node:18-alpine AS builder
WORKDIR /app

# Copy root package.json + lock file
COPY ../package.json ../package-lock.json ./

# Install root dependencies (if needed)
RUN npm install --frozen-lockfile

# Copy frontend source
COPY . .

RUN npm run build

# ------------------------
# 2. Production Stage
# ------------------------
FROM node:18-alpine AS runner
WORKDIR /app

ENV NODE_ENV=production
ENV PORT=3000

COPY --from=builder /app/.next ./.next
COPY --from=builder /app/public ./public
COPY --from=builder /app/package.json ./
COPY --from=builder /app/node_modules ./node_modules

EXPOSE 3000
CMD ["npm", "start"]
