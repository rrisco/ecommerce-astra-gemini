# Ecommerce GenAI powered by DataStax Astra DB Vector

## Before you start

This project is bases in Javascript and Typescript. It also uses React framework NextJS.
Before doing anything else you should install the required dependencies (inside the root directory of the project): 

```bash
nmp install
```

### Create GCP Project in order to use Gemini

1. Create Project
2. Activate Vertex AI APIs
3. Create Service Account and give permission to use Vertex APIs

### Create Astra DB vector database

1. Login or signup with Datastax
2. Create a new vector database

### Creata a local environment file to try the project

1. Create a .env.local file, the values in the file will be used to authenticate the user 
2. Put a value for NEXT_PUBLIC_APP_USER
3. Put a value for NEXT_PUBLIC_APP_PASS

* This is just for trying the app, a proper Authentication method as OAuth or OIDC should be always used when not in a local environment. 

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

## Loading the Data

The product dataset is available on Kaggle: https://www.kaggle.com/datasets/PromptCloudHQ/flipkart-products

The loading process was done using the Jupyter notebook: ./data/Ecommerce multimodal with Gemini.ipynb

THe data is loaded on the collection "ecommerce_prodcuts"

## Embeddings

To generate the embeddings, I used the model "multimodalembedding@001", from GCP Gemini. 

This model returns two embeddings, for image and text. The first image of the product was used to generate the image embedding. The product_name was used to generate the text embedding. Then, the embeddings were balanced and stored on the collection.

The multimodal embedding generation is available on Python SDK, but not on the JavaScript SDK. That's why it was required to generate it using REST request in the API.

## Running the app

Copy the .env_sample to .env.

At GCP, create a service account, with permissions for the Vertex AI API, and generate a credential file. The path of the file 

## Use cases

### Text search

As the text and image embeddings are generated in the same vector space, it is possible to write queries like

```
social shirts for man
```

This will convert the query in an embedding, which will be used for the vector search on Astra.

### Image search

In the same way we can use an image for finding similar products. Just upload a picture ou take a photo and do the search.

### Multi modal search

It is possible to combine image and text. Take a photo and add more characteristics you are looking for.

### Recommendation

Once you find a product, we can suggest similar products. This is done on the products page.
