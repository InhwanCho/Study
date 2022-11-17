
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
#data['Close'] = np.where(data['Close'].isnull(), pd.Series(pred.flatten()), data['Close'])
pd.Series(pred)
```

### pandas datatime 뽑아오기
```python
train['datetime'] = pd.to_datetime(train['datetime'])
train['year'] = train['datetime'].dt.year
train['hour'] = train['datetime'].dt.hour
train['weekday'] = train['datetime'].dt.weekday
```

### ols(다중 공선성) 파악하기
```python
from statsmodels.formula.api import ols
model = ols('target ~ sat + weight + width', df) #열 이름(target,나머지)
res = model.fit()
res.summary()
```

### 특성공학(feature engineering)
```python
train['idle'] = train[['atemp','windspeed','humidity']].apply(lambda x : 
                (0, 1)[x['atemp'] > 22 and x['windspeed'] < 30 and x['humidity'] <50], axis = 1)
```

### boxcox(skew를 균등하게 만들어줌)
```python
from scipy.stats import boxcox 
train['Wind_speed_log'] ,lam= boxcox(train['windspeed'].values +1)
test['Wind_speed_log'] = boxcox(test['windspeed'].values+1, lam)
```

### PCA(차원축소) - 임시?
```python
X = df[['calory', 'breakfast', 'lunch', 'dinner', 'exercise']]
Y = df[['body_shape']]
x_std = StandardScaler().fit_transform(X)
features = x_std.T #(중요)
covariance_matrix = np.cov(features)
eig_vals, eig_vecs = np.linalg.eig(covariance_matrix)
projected_X = x_std.dot(eig_vecs.T[0]) / np.linalg.norm(eig_vecs.T[0])
```

- RS모델, knn for문 따오기