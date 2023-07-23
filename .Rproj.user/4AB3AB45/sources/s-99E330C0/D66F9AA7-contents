library(httr)
library(jsonlite)

# Treasure Hunt
custom_headers = c("Accept" = "*/*",
  "Accept-Encoding" = "gzip, deflate, br",
  "Accept-Language" = "en-US,en;q=0.9",
  "Cookie" = "pgv_pvid=343610618; _ga=GA1.2.1271632362.1690141145; _gid=GA1.2.1930008746.1690141145; Hm_lvt_9cbea5ed9eee7f598e7eb3c4ded861ca=1690141147; Hm_lpvt_9cbea5ed9eee7f598e7eb3c4ded861ca=1690141147; _ga_C968YP88G1=GS1.1.1690141145.1.1.1690141156.0.0.0",
  "Referer" = "https://yobang.tencentmusic.com/chart/uni-chart/detail/?uniId=247595557",
  "Sec-Ch-Ua" = "\"Not/A)Brand\";v=\"99\", \"Google Chrome\";v=\"115\", \"Chromium\";v=\"115\"",
  "Sec-Ch-Ua-Mobile" = "?0",
  "Sec-Ch-Ua-Platform" = "\"macOS\"",
  "Sec-Fetch-Dest" = "empty",
  "Sec-Fetch-Mode" = "cors",
  "Sec-Fetch-Site" = "same-origin",
  "User-Agent" = "Mozilla/5.0"
)


url <- "https://yobang.tencentmusic.com/unichartsapi/v1/songs/247595557/charts_detail"
response <- GET(url, headers = custom_headers)

# Check if the request was successful (status code 200)
if (http_status(response)$category == "Success") {
  json_data = content(response, "text")
  parsed_json = fromJSON(json_data)$data
  
  out_data = as.data.frame(t(c(
    parsed_json$updateTime,
    parsed_json$nextUpdateTime, 
    parsed_json$curRank,
    parsed_json$uniIndex,
    parsed_json$classifyIndices[[1]]$index)))
  
  colnames(out_data) =  c('时间','下次更新','排名','分数','播放','传播','喜好','畅销','推荐')
  
  write.table(out_data, "data/Song1.csv", 
              row.names = FALSE,col.names = FALSE, append = TRUE)
  

} else {
  cat("Request failed with status code:", http_status(response)$status_code, "\n")
}



