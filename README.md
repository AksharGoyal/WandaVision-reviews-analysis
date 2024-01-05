# StackUp Bounty Project: WandaVision reviews analysis  

This is a Data Analysis project that uses data science software such as Pandas and NLTK to clean and prepare the data for analysis of the sentiments behind the reviews.  

For StackUp's Sentiment Analysis Bounty, the show WandaVision (the very first TV show in the MCU franchise on Disney+) was picked to have its reviews analyzed. To get the ball running, the HTML document of the review had to be studied to get an idea of how to extract maximum reviews because, by default, reviews would stop being extracted before the Load More button. Using Selenium's webdriver, it was possible to click on Load More button automatically to get "all" the necessary information. The below code shows how the code helped in unfolding the whole webpage:
```py
try:
    # Wait for the next "Load More" button to become clickable
    load_more_button = WebDriverWait(driver, time_wait).until(
        EC.element_to_be_clickable((By.CLASS_NAME, 'ipl-load-more__button'))
    )
    time_wait += 5
    time.sleep(10)
    # Click the "Load More" button repeatedly until it's no longer visible
    while load_more_button.is_displayed():
        load_more_button.click()
```  

After necessary information (dates of reviews, ratings, reviews, headlines of reviews) was collected, the data had to be cleaned to ensure data integrity was maintained. For example, the list of headlines had space as an extra headline which had to be removed so that all sets had the same length. Null values had to be either removed or filled in with some value. Empty reviews where ratings were 8 or above were replaced with highly positive feedback about the show to make up for it. Emojis had to be removed as they were tampering with the sentiment classification.  

The package `texthero` was used to prepare the text for analysis, and `nltk` was used to automatically analyze the text and derive the sentiment behind the text. As the show is around magic, some words such as 'creepy' and 'mad' had to be given a different score so the sentiment analyzer "Vader" didn't misinterpret the review. Some other words were given different scores to ensure reviews were classified as maximally accurate as possible.

!['Dataframe after cleaning and processing](attachment:image-2.png)

After the data was ready, the reviews were visualized with `texthero` and`plotly` based on what words were frequently used to describe the show or how the ratings and sentiments progressed over the release of the show.  

Overall, it was found that the MCU fans enjoyed the show WandaVision and can't wait for what the future of MCU holds for them.

