FROM ghost:5

# Add app-insights globally
RUN  mkdir /opt/ai && \
        cd /opt/ai && \
        npm init -y && \
        npm install --omit=dev --save applicationinsights && \
        npm install --omit=dev --save applicationinsights-native-metrics

# Copy the ai-bootstrap.js file
COPY ai-bootstrap.js /opt/ai/

# Configure AI via ENV VARS
# ENV APPINSIGHTS_INSTRUMENTATIONKEY xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
# ENV APPLICATIONINSIGHTS_ROLE_NAME Frontend
# ENV APPLICATIONINSIGHTS_ROLE_INSTANCE GhostInstance
# Lets use platform agnositic node method to load AI instead of monkey patching i.e. NODE_OPTIONS='--require "/opt/ai/ai-bootstrap.js"'
ENV NODE_OPTIONS='--require /opt/ai/ai-bootstrap.js'