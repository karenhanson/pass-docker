FROM openjdk:8u151-jre-alpine3.7

ENV NOTIFICATION_SERVICES_VERSION=0.0.2-3.2 \
    JSONLD_CONTEXT_VERSION=3.2 \
    FCREPO_HOST=${FCREPO_HOST:-fcrepo} \
    FCREPO_PORT=${FCREPO_PORT:-8080} \
    FCREPO_JMS_PORT=${FCREPO_JMS_PORT:-61616} \
    ES_HOST=${ES_HOST:-elasticsearch} \
    ES_PORT=${ES_PORT:-9200} \
    PASS_FEDORA_USER=${PASS_FEDORA_USER:-fedoraAdmin} \
    PASS_FEDORA_PASSWORD=${PASS_FEDORA_PASSWORD:-moo} \
    PASS_ELASTICSEARCH_LIMIT=${PASS_ELASTICSEARCH_LIMIT:-100} \
    NOTIFICATION_DEBUG_PORT=${NOTIFICATION_DEBUG_PORT:-5011} \
    PASS_NOTIFICATION_MODE=${PASS_NOTIFICATION_MODE:-DEMO} \
    PASS_NOTIFICATION_QUEUE_EVENT_NAME=${PASS_NOTIFICATION_QUEUE_EVENT_NAME:-event} \
    PASS_NOTIFICATION_SMTP_HOST=${PASS_NOTIFICATION_SMTP_HOST:-localhost} \
    PASS_NOTIFICATION_SMTP_PORT=${PASS_NOTIFICATION_SMTP_PORT:-587} \
    PASS_NOTIFICATION_CONFIGURATION=${PASS_NOTIFICATION_CONFIGURATION:-file:/notification.json} \
    NOTIFICATION_OPTS=""

RUN apk update && \
    apk add --no-cache wget && \
    wget -O notification-services.jar \
        http://repo1.maven.org/maven2/org/dataconservancy/pass/notify/notification-boot/${NOTIFICATION_SERVICES_VERSION}/notification-boot-${NOTIFICATION_SERVICES_VERSION}-exec.jar

COPY entrypoint.sh /

RUN chmod 700 /entrypoint.sh

COPY notification.json /notification.json

COPY templates/ /templates

ENV JAVA_TOOL_OPTIONS -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=${NOTIFICATION_DEBUG_PORT}

ENTRYPOINT [ "/entrypoint.sh" ]