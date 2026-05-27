Bronze bucket name : yt-datapipeline-bronze-ap-south-1-dev
Silver bucket name : yt-datapipeline-silver-ap-south-1-dev 
Gold bucket name : yt-datapipeline-gold-ap-south-1-dev  

script bucket name : yt-datapipeline-script-ap-south-1-dev

SNS ARN - arn:aws:sns:ap-south-1:619924817423:yt-datapipeline-alerts-dev:dc445720-bd40-4971-b9d8-97b75451dd83
arn:aws:sns:ap-south-1:619924817423:yt-datapipeline-alerts-dev

Glue Bronze - yt-pipeline-bronze-dev
Glue Silver - yt-pipeline-silver-dev
Glue Gold - yt-pipeline-gold-dev


--bronze_database yt-pipeline-bronze-dev
--bronze_table raw_statistics
--silver_bucket yt-datapipeline-silver-ap-south-1-dev 
--silver_database yt-pipeline-silver-dev
--silver_table clean_statistics


--silver_database yt-pipeline-silver-dev
--gold_bucket yt-datapipeline-gold-ap-south-1-dev
--gold_database yt-pipeline-gold-dev

