FROM ghost:5-alpine AS depbuild

RUN apk add --update --no-cache \
    python3 \
    build-base 

WORKDIR /opt/ai

RUN npm init -y && \
        npm install --omit=dev --save applicationinsights && \
        npm install --omit=dev --save applicationinsights-native-metrics@0.0.6

FROM ghost:5-alpine

WORKDIR /opt/ai

# Copy the ai-bootstrap.js file
COPY ai-bootstrap.js .
COPY --from=depbuild /opt/ai .

# Configure AI via ENV VARS
# ENV APPINSIGHTS_INSTRUMENTATIONKEY xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
# ENV APPLICATIONINSIGHTS_ROLE_NAME Frontend
# ENV APPLICATIONINSIGHTS_ROLE_INSTANCE GhostInstance
# Lets use platform agnositic node method to load AI instead of monkey patching i.e. NODE_OPTIONS='--require "/opt/ai/ai-bootstrap.js"'
ENV NODE_OPTIONS='--require /opt/ai/ai-bootstrap.js'