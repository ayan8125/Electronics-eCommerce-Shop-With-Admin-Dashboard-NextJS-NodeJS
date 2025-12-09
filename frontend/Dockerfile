# ------------------------
# 1. BUILD STAGE
# ------------------------
FROM node:18-alpine AS builder
WORKDIR /app

# Copy ONLY frontend files (because build context = frontend folder)
COPY package.json package-lock.json ./
RUN npm install --frozen-lockfile

COPY . .

RUN npm run build

# ------------------------
# 2. RUNNER STAGE
# ------------------------
FROM node:18-alpine AS runner
WORKDIR /app

ENV NODE_ENV=production
ENV PORT=3000

COPY --from=builder /app ./

EXPOSE 3000
CMD ["npm", "start"]
