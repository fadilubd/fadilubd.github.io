---
layout: post
title: Laporan Magang Minggu Ke-empat - MBKM Bina Darma Unit Kerjasama dan Alumni
date: 2023-10-28 09:00:00 -0400
description: 
tags: laporan mbkm magang
categories: laporan
giscus_comments: false
related_posts: false
---
[https://www.binadarma.ac.id/](https://www.binadarma.ac.id/)

### Senin - Kamis, 23-26 Oktober 2023
- Membuat grup WhatsApp untuk 600 calon wisudawan 2023
  1. Mengubah daftar calon wisudawan ke google contacts CSV
    ```python
    import pandas as pd
    import regex as re
    from io import StringIO
    xl_file = pd.ExcelFile("wisudawan.xlsx")
    
    for prodisheet in xl_file.sheet_names:
      csvheaders='''Name,Given Name,Additional Name,Family Name,Yomi Name,Given Name Yomi,Additional Name Yomi,Family Name Yomi,Name Prefix,Name Suffix,Initials,Nickname,Short Name,Maiden Name,Birthday,Gender,Location,Billing Information,Directory Server,Mileage,Occupation,Hobby,Sensitivity,Priority,Subject,Notes,Language,Photo,Group Membership,Phone 1 - Type,Phone 1 - Value,E-mail 1 - Type,E-mail 1 - Value'''
      if(prodisheet == "Sheet2"): continue
      data =  pd.read_excel('wisudawan.xlsx',sheet_name=prodisheet,header=4)
      csvh = pd.read_csv(StringIO(csvheaders))
    
      for entry in data.values:
        print(entry)
        phonenumber = re.split(r'[^0-9+]+',re.sub('-','',str(entry[4])))[0]
        print(entry[4],'===',phonenumber)
        csvh.loc[len(csvh)] = {
            'Name': f"{entry[2]} - {entry[1]} - {entry[3]} - Calon Wisudawan 2023",
            'Phone 1 - Value': phonenumber,
            'E-mail 1 - Value': entry[5]
        }
      csvh.to_csv(f"out/Kontak Calon Wisudawan 2023 - {prodisheet}.csv", index=False)
    ```
  2. Mengupload file csv ke google contacts
  3. Membuat grup WhatsApp dan mengundang calon wisudawan sesuai program studi 
### Jumat - Sabtu, 27-28 Oktober 2023
- Menyelesaikan tracer 2022
  - Menguba data dari google form ke format tracerstudy kemendikbut
  - Mengupload file ke tracerstudy

