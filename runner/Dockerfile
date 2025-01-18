# 使用 Node.js 作为基础镜像
FROM node:22-slim

# 安装 pnpm
RUN npm install -g pnpm

# 设置工作目录
WORKDIR /app

# 复制 package.json 文件
COPY package.json pnpm-lock.yaml ./
COPY apps/readest-app/package.json ./apps/readest-app/
COPY packages/foliate-js/package.json ./packages/foliate-js/

# 安装依赖
RUN pnpm install

# 复制源代码
COPY . .

# 设置构建参数
ARG NEXT_PUBLIC_POSTHOG_KEY
ARG NEXT_PUBLIC_POSTHOG_HOST
ARG NEXT_PUBLIC_DEEPL_API_KEY
ARG NEXT_PUBLIC_SUPABASE_URL
ARG NEXT_PUBLIC_SUPABASE_ANON_KEY

# 设置环境变量
ENV NEXT_PUBLIC_POSTHOG_KEY=$NEXT_PUBLIC_POSTHOG_KEY
ENV NEXT_PUBLIC_POSTHOG_HOST=$NEXT_PUBLIC_POSTHOG_HOST
ENV NEXT_PUBLIC_DEEPL_API_KEY=$NEXT_PUBLIC_DEEPL_API_KEY
ENV NEXT_PUBLIC_SUPABASE_URL=$NEXT_PUBLIC_SUPABASE_URL
ENV NEXT_PUBLIC_SUPABASE_ANON_KEY=$NEXT_PUBLIC_SUPABASE_ANON_KEY
ENV NEXT_PUBLIC_APP_PLATFORM=web

# 设置 PDF.js
RUN cd apps/readest-app && pnpm setup-pdfjs

# 构建应用
RUN cd apps/readest-app && pnpm build-web

# 暴露端口
EXPOSE 3000

# 启动命令
CMD ["pnpm", "--filter", "@readest/readest-app", "start-web"] 