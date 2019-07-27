# ZS-Data-Science-Challenge-2019

The process is as shown below:

### Data Prep:
1. The data was first explored in excel and the index column was deleted.
2. Missing values were found for the shot_id_number column and were filled in using excel autocomplete feature.
3. The data was loaded into a pandas dataframe with 27 columns
4. The remaining_min and remaining_sec columns with NaN values were replaced with 0 as if the column is black it is safe to assume that it is not required.
5. Several columns which were not required or were not providing meaningful insights or were providing incorrect data were deleted namely team_name, team_id, match_event_id, date_of_game, remaining_min.1, power_of_shot.1, knockout_match.1, remaining_sec.1 and distance_of_shot.1
6. lat/lng were backfilled as it has only 38 unique different values and they were highly correlated with the previous value.
7. The lat/lng, remaining_min and remaining_sec column were deleted after creating remaining_time and is_home features from them.
8. home/away was filled by defining a function change_value which filled Nan values with their respective values using the column match_id
9. game_season, knockout_match, power_of_shot were backfilled as a single match will have the same data for all of these values and backfilling them will produce desirable results with minimal error.
10. match_id was dropped after being used for the above features.
11. location_x, location_y, distance_of_shot NaN values were filled with their respective means.
12. area_of_shot, shot_basics, range_of_shot were iteratively filled alternating between modify function and their modes or backfills.
13. After all NaN values were removed, all categorical values were changed using LabelEncoder.
14. StandardScaler was applied to transform the data into a probability distribution.
15. The shot_id_number was replaced as the index.
16. The test data and the training data was separated.
17. The training data was further split into 30% validation data using train_test_split.

### EDA:
1. The value_counts() of lat/lng gave us the insight of making another feature of whether the match was played at home ground or not using the value. This is different from home/away feature as in that we tried to explore the scoring ability of Ronaldo against various teams and not whether he played well at home or away ground.
2. remaining_time is created using remaining_min and remaining_sec
3. type_of_shot  was created by combining the columns of its namesake and type_of_combined_shot since they were complementary to each other at every example.
4. The values of the remaining columns with NaN columns were explored to decide what to fill them with.
5. Using excel, relations were found between area_of_shot, shot_basics, range_of_shot and were implemented in the function modify.
6. Data were explored for skewness and correlations using various plots.
7. Dummies were created for every categorical column with non-numerical significance.
8. Functions algo and algo_final were created to use various classifiers without and with StratifiedKFold respectively.

### Model Building:
1. 8 various classifiers were tested on the basis of their accuracy and validation scores using StratifiedKFold namely LogisticRegression, SGDClassifier, GaussianNB, KNeighborsClassifier, DecisionTreeClassifier, RandomForestClassifier, SVC and xgboost.
2. After their individual accuracies were determined, lesser performing algorithms were ignored and the rest were checked with GridSearchCV and were evaluated on various parameters.
3. XGBClassifier, LogisticRegression, and DecisionTreeClassifier were the best performing algorithm and were deployed to make a submission.
4. Ensemble techniques were used to combine their probability predictions.
5. After the above tasks, a Neural Network Model was trained which surpassed its predecessor.

### Conclusion:
The model was built on Keras Neural Network. A detailed model was prepared by training the data with 8 different classifiers along with a Neural Network and choosing the best out of them, also, combined with the best parameters. The process was mainly compromised of two major tasks that involved cleaning and preparing the data which was then deployed after achieving satisfactory results. Lastly, ensemble techniques were used to better the predictability of values but the Neural Network was better than the techniques and hence, was deployed.
