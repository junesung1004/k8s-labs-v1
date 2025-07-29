# Step 1: Build 단계
FROM node:18-alpine AS builder

WORKDIR /app

COPY . .         
RUN npm install
RUN npm run build --no-lint

# Step 2: 실행 단계
FROM node:18-alpine AS runner

WORKDIR /app

COPY --from=builder /app .  

EXPOSE 3000

CMD ["npm", "start"]