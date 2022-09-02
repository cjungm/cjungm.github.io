---
title: S3 Create Foler
author: J.M
date: 2022-08-16
category: S3
layout: post
---

S3에 대한 흔한 착각인데 S3는 Object Storage 이므로 폴더라는 개념이 존재하지 않습니다. 

하지만 Console에는 "**create folder**" 라는 기능이 있는데 이는 0 byte object를 생성하는 행위입니다.

따라서 삭제 시에도 Object 삭제와 동일하게 접근해야 합니다.

파일을 S3 Object를 삭제하다 보면 하위에 object가 없는 경로들은 자동으로 삭제되는 데 가끔 유지되는 경로들을 발견하신 적이 있다면 해당 경로들은 명시적으로 생성했던 object인 것입니다.

예) 특정 버킷 "test_path" 하위에 "test.csv"를 등록 및 삭제할 때
 1. "create folder"를 수행하지 않고 등록
    등록 시 : s3://{bucket_name}/test_path/test.csv 
    삭제 시 : s3://{bucket_name} (경로까지 삭제 됨)

 2. "create folder"를 수행 후 등록
    등록 시 : s3://{bucket_name}/test_path/test.csv 
    삭제 시 : s3://{bucket_name}/test_path ("test_path"는 경로가 아닌 Object 이므로 유지됨)

    

[참조](https://blog.dataminded.com/the-mystery-of-folders-on-aws-s3-78d3428803cb)
