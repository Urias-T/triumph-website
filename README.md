# A Simple Guide

This guide explains the steps I'll recommend if you want to build your static website and set up a CI/CD pipeline for it, based on my own experience.

1. Choose a template. (I got mine from [StyleShout]( https://styleshout.com/category-template/portfolio/))
2. Download the template and edit with your preferred IDE/ code editor (Remember to verify responsiveness. If you use VSCode, [this](https://youtu.be/uRYHX4EwYYA?si=pKrq0MiaX5CaU8cU) can be helpful).
3. Push to GitHub.
4. Purchase your domain (I purchased mine on [CloudFlare](https://www.cloudflare.com/)).
5. Start a GCP project and create a storage bucket. ([How To](https://cloud.google.com/storage/docs/creating-buckets)).
   - The bucket should be named with the domain you intend to use for your website (ie. the one you purchased above).
   - Follow the prompts to verify that you own this domain (through Google Search Console).
       - This verification would automatically modify your domain's DNS records.
   - You want uniform access control on your bucket.
   - Bucket should be publicly accessible. ([How To](https://cloud.google.com/storage/docs/access-control/making-data-public)).
6. Create a service account to be used by the GitHub workflow for CI/CD. ([How To](https://cloud.google.com/iam/docs/service-accounts-create#iam-service-accounts-create-console)).
   - This account should have permission to write to your GCS bucket.
   - Copy the credentials and keys for this service account and save as secret in GitHub ([How To](https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions)).
       - Include the name of your bucket in the secrets as well. (Optional)
7. Write the GitHub workflow and include it in the `.github/workflows` directory. [Cloud Storage Uploader](https://github.com/marketplace/actions/cloud-storage-uploader)
8. Modify your DNS records:
   - Set a CNAME record for the root to point to `storage.googleapis.com`.
   - Set a CNAME record for `www` to point to `storage.googleapis.com`.
     - Now you would need to setup a page forwarding rule for `www` to forward to the root.

PS: If you have any questions and/ or contributions to make to these steps, please forward such to me at: triumph@triumphurias.com
  


