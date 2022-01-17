#!/bin/bash
# -------------------------------------------------------------------------------------------
# Author: Alex T. CEO/CTO IdeaUP
# Allow to connect, register and push a new container to GCP container registry. 
# -------------------------------------------------------------------------------------------

CONTAINER_NAME="your-container-name"
IMAGE_ID="your-container-image-id"
TAG="your-tag-of-your-docker-image"
PROJECT_ID="your-project-id-in-google-cloud-platform"
# if you want to use -f for build a docker image in another path
#docker_file_path="../../../../../DockerFile"

# Docker commands:
DOCKER_BUILD=$(docker build -t ${IMAGE_ID} .);
DOCKER_TAG=$(docker tag ${IMAGE_ID} gcr.io/${PROJECT_ID}/${IMAGE_ID}:${TAG});
DOCKER_PUSH_TO_REGISTRY=$(docker push gcr.io/${PROJECT_ID}/${IMAGE_ID}:${TAG});

echo "Building docker image..."
if [[ ${DOCKER_BUILD} ]]; then

    echo  "Finishing docker build process"
    echo "Starting a new container registry for " ${CONTAINER_NAME}

    docker tag ${IMAGE_ID} gcr.io/${PROJECT_ID}/${IMAGE_ID}:${TAG}
    echo "Successfully tagged docker image"
    echo "Trying to push image to GCP container registry"

    if [[ ${DOCKER_PUSH_TO_REGISTRY} ]]; then
            echo "Successfully pushed docker container image" ${IMAGE_ID}
            gcloud container images list --repository=gcr.io/${PROJECT_ID}

            exit 0
    else
            echo "Error. Not able to push image into GCP container registry"
            exit 2
    fi

#    if [[ ${DOCKER_TAG} ]]; then
#        echo "Successfully tagged docker image"
#        echo "Trying to push image to GCP container registry"
#
#        if [[ ${DOCKER_PUSH_TO_REGISTRY}]]; then
#            echo "Successfully pushed docker container image" ${IMAGE_ID}
#            exit 0
#        else
#            echo "Error. Not able to push image into GCP container registry"
#            exit 2
#        fi

else
    echo "Error. Cannot build image."
    exit 2
fi
