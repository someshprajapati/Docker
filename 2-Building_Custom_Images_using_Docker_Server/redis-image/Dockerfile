# Use an existing docker image as base
FROM alpine

# Download and install depedency
RUN apk add --update redis

# Tell the image what to do when start as container 
CMD ["redis-server"]
