```
%%time
### 실험중
# 수집할 글 갯수 정하기
user_list=[]
rev_count_list=[]
driver = webdriver.Chrome(chrome_path)

# 수집한 url 돌면서 데이터 수집
for k in tqdm_notebook(range(0,len(df_load))):
        
    # 리뷰창 띄우기
    driver.get(url)   
    time.sleep(2)

    
    for j in range(0,20):
        try:
            
            for i in range(0, 10):
                # 유저아이디링크따기
                userid =".customer-profile-link"
                user=driver.find_elements_by_css_selector(userid)
                userurl=user[i].get_attribute('href')
                user_list.append(userurl)

                #유저리뷰수 따기
                rev_count=driver.find_elements_by_css_selector(".snapshot-count")
                rev_count_list.append(rev_count)

                if i == 9:
                    pg_nx= driver.find_element_by_css_selector(".paging-btn-next")
                    driver.execute_script("arguments[0].click();", pg_nx)
                    time.sleep(2)
        except: 
            input('Y/N')
            
            for i in range(0, 10):
                userid =".customer-profile-link"
                user=driver.find_elements_by_css_selector(userid)
                userurl=user[i].get_attribute('href')
                user_list.append(userurl)

                #유저리뷰수 따기
                rev_count=driver.find_elements_by_css_selector(".snapshot-count")
                rev_count_list.append(rev_count)

                if i == 9:
                    pg_nx= driver.find_element_by_css_selector(".paging-btn-next")
                    driver.execute_script("arguments[0].click();", pg_nx)
                    time.sleep(2)
            
    print(k,df_load.item_id[k],review_count)
    driver.close()
```

