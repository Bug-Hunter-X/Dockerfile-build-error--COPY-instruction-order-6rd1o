# Dockerfile Build Error: Incorrect COPY Instruction Order

This repository demonstrates a common error when building Docker images with Node.js applications. The error is caused by copying the application code before installing the dependencies, resulting in the build failing.

## Bug

The original `Dockerfile` has the `COPY . .` instruction before `RUN npm install`. This leads to a failure as the `npm install` command won't find the `package.json` file. 

## Solution

The fixed `Dockerfile.fixed` corrects the order to first copy `package*.json`, then run `npm install`, and finally copy the rest of the application code. This ensures the dependencies are installed before attempting to build the application.

## Steps to reproduce

1. Clone the repository.
2. Build the original Dockerfile: `docker build -f Dockerfile -t my-app .` (This will fail)
3. Build the fixed Dockerfile: `docker build -f Dockerfile.fixed -t my-app .` (This will succeed)