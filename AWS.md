# S3で画像を保存する  
 IaC(Infrastructure as Code) サーバーなどのインフラ環境ををCLIを用いて管理すること  
## AWS CloudShellを用いてバケットを作成し、セキュリティ対策をする(ex,バケット名：furima40467)  
- バケットを作成する  
-- aws s3 mb s3://バケット名  
- バケットが作成できたか確認する  
-- aws s3 ls  
