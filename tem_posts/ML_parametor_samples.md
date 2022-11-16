
### SVR
```python
svr = SVR(kernel='poly')
params = [{
    'C' : [0.5, 1, 3, 5, 7],
    'gamma' : [0.01,0.25,0.5,0.75, 1]
}]
grid = GridSearchCV(svr,param_grid=params,cv = 2)
grid.fit(x_train,y_train)
svr_best = grid.best_estimator_
ypred = grid.predict(x_test)
# mean_absolute_error(ypred,y_test)
```

### Randomforest

```python
### RandomForestRegressor()
rf = RandomForestRegressor()
params = {
    'n_estimators':[50,70,100],
    'max_depth' : [13,15,18,20], 
    'min_samples_leaf' : [2,5,10,17,19],
    'min_samples_split' : [2,3,4],
    'max_features' : [3,5,10,15]
}
rf_cv = GridSearchCV(rf , param_grid=params , cv=5, n_jobs=-1 )
rf_cv.fit(x_train , y_train)
rf_best = rf_cv.best_estimator_

ypred = rf_best.predict(x_test)
```

### VotingClassifier
```python
vote = VotingClassifier(estimators = [('RF',rf),('LR',lr),('KNN',knn)] , voting = 'soft')
vote.fit(x_train,y_train)
ypred = vote.predict(x_test)
print(f'voting score : {accuracy_score(ypred,y_test)}')
pred = vote.predict(df_test)
```

### LogisticRegression
```python
grid = {'C':np.logspace(-3,3,7), 'penalty':['l1','l2','l3']}
lr_cv = GridSearchCV(logreg,grid,cv=10)
lr_cv.fit(x_train,y_train)
lr_best = lr_cv.best_estimator_
ypred = lr_best.predict(x_test)
pred = lr_best.predict(df_test)
print(f'logistic score : {accuracy_score(ypred,y_test)}')
```

### KNeighborsClassifier    n_neighbors==7이 가장 높음
```python
knn.fit(x_train,y_train)
ypred = knn.predict(x_test)
pred = knn.predict(df_test)
print(f'knn score : {accuracy_score(ypred,y_test)}')
```

### 다중 선형회귀 샘플
```python
from sklean.linear_model import LinearRegression
df['whole_weight'].iloc[:3] = np.nan
X = df[['diameter','shell_weight','height']].iloc[3:]
y = df['whole_weight'].iloc[3:]
lin = LinearRegression()
lin.fit(X,y)
pred = lin.predict(df[['diameter','shell_weight','height']])
df['whole_weight'].fillna(pd.Series(pred))
pd.Series(pred)
```

### 야후 증권 데이터 따오기
```python
```

- RS모델, knn for문 따오기