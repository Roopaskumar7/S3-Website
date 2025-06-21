

✅ README.md

```markdown
# 🌐 AWS S3 + Cloudflare + GitHub Actions - Static Website

This project demonstrates how to host and automatically deploy a **static website** using:

- ✅ **Amazon S3** – for storage and hosting
- ✅ **Cloudflare** – for CDN, HTTPS, and DNS
- ✅ **GitHub Actions** – for continuous deployment on every `git push`

---

## 📂 Folder Structure

```

S3-Website/
├── index.html
├── style.css
├── screenshot.png
├── deployment\_report.md
└── .github/
└── workflows/
└── deploy.yml

````


---

## 🛠️ Deployment Workflow

Every time you push to `main`:
1. GitHub Actions runs `deploy.yml`
2. Your files are synced to the S3 bucket
3. (Optional) Cloudflare cache is purged

GitHub Secrets used:
- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `CLOUDFLARE_ZONE_ID` (optional)
- `CLOUDFLARE_API_TOKEN` (optional)

---

## ☁️ S3 Configuration

1. **Create a bucket**  
   - Bucket name: `your-s3-bucket-name`
   - Region: `ap-south-1` (or your region)
   - Uncheck **Block all public access**

2. **Enable static website hosting**  
   - Index document: `index.html`

3. **Add this bucket policy**:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-s3-bucket-name/*"
    }
  ]
}
````

Enable:

* ✅ Proxy Status: **Proxied**
* ✅ SSL/TLS → **Full**
* ✅ Always Use HTTPS

---

## 🤖 GitHub Actions CI/CD

`.github/workflows/deploy.yml`:

```yaml
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ap-south-1
      - uses: jakejarvis/s3-sync-action@master
        with:
          args: --delete
        env:
          AWS_S3_BUCKET: github-user
          AWS_REGION: N.Virgina-1
```


## 📬 Contact

For questions, raise an issue or reach out at:
📧 [roopaskumar7@gmail.com](mailto:roopaskumar7@gmail.com)

---

> 💡 This project is beginner-friendly and helps understand modern CI/CD & static hosting with AWS.




