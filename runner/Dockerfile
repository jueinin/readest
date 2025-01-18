FROM node:22-slim

RUN npm install -g pnpm mkdirp

WORKDIR /app

COPY . .

RUN pnpm install && pnpm --filter @readest/readest-app setup-pdfjs

ARG NEXT_PUBLIC_SUPABASE_URL
ARG NEXT_PUBLIC_SUPABASE_ANON_KEY

ENV NEXT_PUBLIC_SUPABASE_URL=$NEXT_PUBLIC_SUPABASE_URL
ENV NEXT_PUBLIC_SUPABASE_ANON_KEY=$NEXT_PUBLIC_SUPABASE_ANON_KEY
ENV NEXT_PUBLIC_APP_PLATFORM=web

RUN cd apps/readest-app && pnpm build-web

EXPOSE 3000

CMD ["pnpm", "--filter", "@readest/readest-app", "start-web"] 