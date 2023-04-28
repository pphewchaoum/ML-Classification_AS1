# ML-Classification_AS1
Project Firewall database

##1. Get data from log file link https://www.kaggle.com/datasets/tunguz/internet-firewall-data-set

Fatih Ertam (2018) ได้วิเคราะห์ข้อมูลการบันทึกบนอุปกรณ์ไฟร์วอลล์และควบคุมการรับส่งข้อมูลทางอินเทอร์เน็ตตามผลการวิเคราะห์ที่มาจากการบันทึกการใช้อุปกรณ์ไฟร์วอลล์ของ Firat University ซึ่งจำแนกข้อมูลออกเป็น 4 คลาส allow deny drop และ reset-both โดยใช้วิธี SVM ได้แก่ Linear, Polynomial, Sigmoid และ RBF วัดประสิทธิภาพของแบบจำลองโดยใช้ Precesion recall และ  F1-score เราสามารถระบุได้ว่าข้อมูลที่สร้างขึ้นจากการจัดหมวดหมู่มีความเกี่ยวข้องกับข้อมูลที่ตั้งใจไว้มากน้อยเพียงใด ในการศึกษานี้ ใช้ 11 ลักษณะ ในการวิเคราะห์ข้อมูลเหตุการณ์จำนวน 65,532 ครั้ง ตามตารางด้านล่างนี้ 
	
<p align="center">
  <img width="400" height="400" src="https://user-images.githubusercontent.com/122291438/235178139-78356fc9-1c01-4ac2-80aa-adf48f618edf.png">
</p>



SVM+Sigmoid ให้ค่า recall สูงสุด 98.5%  ส่วน SVM+Linear ให้ค่า precision สูงสุดที่ 67.5% และ SVM+RBF ให้ค่าคะแนน F1 สูงสุดที่ 76.4% ในขณะที่ SVM+Polynomial ให้ค่า precision และ recall อยู่ในระดับต่ำ เมื่อใช้ค่าเฉลี่ย จะเห็นได้ชัดว่าตัวแยกประเภทตามฟังก์ชันการเปิดใช้งาน SVM+RBF นั้นดีที่สุด สำหรับแต่ละคลาส (Table III.)
	
<p align="center">
  <img width="400" height="100" src="https://user-images.githubusercontent.com/122291438/235179021-07bb4b52-393c-4d03-bcd3-7ae82aafc8d7.png">
</p>

ข้อจำกัดในงานวิจัยนี้คือ SVM ใช้เพื่อจัดการปัญหาที่เกี่ยวข้องกับสองคลาสขึ้นไป ไม่เหมาะกับการใช้กับข้อมูลที่มีความสูงต่ำกว่า data point จึงต้องแปลงข้อมูลให้อยู่ใน input space ไปสู่ transformed Space ที่เรียกว่า Feature space จึงสามารถใช้ตัวแบบ SVM ได้ในการแบ่ง ข้อมูลด้วย Hyperplane เช่น Polynomial Kernel, Radial Basis Function(RBF), Sigmoid Kernel 

2. ขั้นตอน Collect data, inspectation data, Data Exploration ( EDA ) 
2.1 จำนวนActionที่เกิดขึ้นในtransaction

	
<p align="center">
  <img width="1000" height="300" src="https://user-images.githubusercontent.com/127765032/235164910-e0f082c4-f042-4aeb-b368-aed89fd65dd6.png">
</p>
		
2.2 การหาค่าmeanของ Elapsed time (sec)
		
<p align="center">
  <img width="1000" height="300" src="https://user-images.githubusercontent.com/127765032/235164916-79592a7a-f093-4f59-b899-5e02bccd2ef8.png">
</p>

2.3 การหาค่า meanของ Bytes

<p align="center">
  <img width="1000" height="300" src="https://user-images.githubusercontent.com/127765032/235164925-3aad5a00-bcb3-4344-8aa0-b0588d5bc8a9.png">
</p>	
		
2.4 การหา correlation ของ Bytes & time แบบไม่ได้ remove bytes ที่เป็นoutliner ออก
2.5 การหา correlation ของ Bytes & time แบบปรับค่า น้อยกว่าเท่ากับ 1000
2.6 การหา correlation ของ Bytes & time แบบปรับค่า น้อยกว่าเท่ากับ 10000
2.7 การหา correlation ของ Bytes & time แบบปรับค่า น้อยกว่าเท่ากับ 100000
	
<p align="center">
  <img width="1000" height="300" src="https://user-images.githubusercontent.com/127765032/235159698-0f0a7407-7860-46f7-a641-0cc8bc192049.png">
</p>		

		3.8 การหา Top Destionation port ที่มีการเกิดtransactionมากที่สุด
		3.9 การหา Top Source port ที่มีการเกิดtransactionมากที่สุด
		
<p align="center">
  <img width="1000" height="500" src="https://user-images.githubusercontent.com/127765032/235161200-675e846d-fd93-4892-aab1-c7ee69c39089.png">
</p>			


		3.10 การหา Correlation heatmap เพื่อดูความสัมพันธ์ของFeature ทุกตัว
<p align="center">
  <img width="1000" height="500" src="https://user-images.githubusercontent.com/127765032/235173429-5b1c5752-d22a-4f45-8c87-b2ed970c338f.png">
</p>		
		

4. Traning Model Tools

		4.1 Cart Method
		จากการrun model Cart จากข้อมูลtest 30% ได้F1 score = 0.9977 20% ได้F1 score = 0.9975 10% ได้F1 score = 0.9971
		#GridSearCV
		tree_clas = DecisionTreeClassifier(random_state=1024)
		param_tree = {'max_features': ['auto', 'sqrt', 'log2'],
			      'ccp_alpha': [0.1, .01, .001],
			      'max_depth' : [3, 4, 5, 6, 7, 8, 9, 10],
			      'criterion' :['gini', 'entropy']}
		grid_tree = GridSearchCV(estimator=tree_clas, param_grid=param_tree, cv=5, verbose=True)
		grid_tree.fit(x_train, y_train)
		grid_tree.best_estimator_
		ans_tree = grid_tree.predict(x_test)
		print(classification_report(y_test, ans_tree))
จากการทำ GridSearchCV ได้ค่าพารามิเตอร์คือ DecisionTreeClassifier(ccp_alpha=0.001, criterion='entropy', max_depth=9, max_features='auto', random_state=1024)

<p align="center">
  <img width="1000" height="300" src="https://user-images.githubusercontent.com/127765032/235169339-deee6f76-2974-409d-a072-1710a4969754.png">
</p>	
	
		4.2 Random Forest
		#GridSearCV
		RT_clas = RandomForestClassifier(n_estimators=100,random_state=1024) 
		param_RT = {'max_features': ['auto', 'sqrt', 'log2'], 
				    'ccp_alpha': [0.1, .01, .001], 
				    'max_depth' : [2,3, 4, 5, 6, 7], 
				    'criterion' :['gini', 'entropy']} 
		grid_RT = GridSearchCV(estimator=RT_clas, param_grid=param_RT, cv=5, verbose=True) 
		grid_RT.fit(x_train, y_train) 
		grid_RT.best_estimator_
		ans_RT = grid_RT.predict(x_test)
		print(classification_report(y_test, ans_RT))
จากการทำ GridSearchCV ได้ค่าพารามิเตอร์คือ RandomForestClassifier(ccp_alpha=0.001, criterion='entropy', max_depth=7, max_features='auto', random_state=1024)
<p align="center">
  <img width="1000" height="220" src="https://user-images.githubusercontent.com/127765032/235181209-5c2e318e-b28e-4b73-8ee3-29237d881562.png">
</p>
	
		4.3 XGBoost
		xgb_cls = xgb.XGBClassifier(use_label_encoder=False, n_estimators=10)
		xgb_cls.fit(x_train, y_train.astype(int))

		ans_xgb = xgb_cls.predict(x_test)
		print(classification_report(y_test, ans_xgb))

		plot_tree(xgb_cls, rankdir='UT', num_trees=1)
		fig = plt.gcf()
		fig.set_size_inches(15, 10)

		plt.show()
		plt.savefig('log2-xgboot.png')

<p align="center">
  <img width="1000" height="200" src="https://user-images.githubusercontent.com/127765032/235181225-9c3f7524-adc7-49d0-926c-a52342fd17d0.png">
  <img width="1000" height="350" src="https://user-images.githubusercontent.com/122291438/235189296-016859a0-4102-456e-bbbb-746c24a53cca.png">
</p>

		
		4.4 K-NN 
	จากการrun modle KNN ค่าF1จาการ testข้อมูล 30% ให้F1 score = 0.9936 ในขณะที่ test 20% ได้F1 score 0.9933 และ F1 score 0.9924
	Test 10% นั้นสะท้อนในให้เห็นว่่ายิ่งมีdataในการtest มากขึ้นยิ่งเพิ่มประสิทธิภาพของmodel
	
	#GridSearCV
	knn = KNeighborsClassifier()
	parameters = {"n_neighbors": range(1,11),
                      "metric": ('minkowski','euclidean','manhattan'),
                      "weights": ('uniform','distance')}
	grid_knn = GridSearchCV(knn, parameters, cv=5)
	grid_knn.fit(x_train,y_train)
	grid_knn.best_estimator_
จากการทำ GridSearchCV ได้ค่าพารามิเตอร์คือ KNeighborsClassifier(metric='manhattan', n_neighbors=1)
<p align="center">
  <img width="1000" height="200" src="https://user-images.githubusercontent.com/127765032/235183406-75751a0d-546c-4f64-bb32-006d02779e66.png">
</p>
	


6.Evaluation

		6.1 F1 Score เทียบผล
		
<p align="center">
  <img width="1000" height="500" src="https://user-images.githubusercontent.com/122291438/235169008-9e32d34a-96b7-4ae5-a718-8c0f09ebd5be.png">
</p>

สรุปผล: จากการทดลอง จะเห็นได้อย่างชัดเจนว่าของ F1 score ของ xgboost มากที่สุด = 99.79% ในขณะที่ Model อื่น average อยู่ที่ 87.99% นอกจากนี้ยังสามารถเพิ่ม
F1 score ของSVM ได้มากกว่าในreport ที่กล่าวมาข้างต้นจากเดิม 76.4 % โดยปรับimblance data และ Feacture scaling (normalization) ใน pycarte F1 score = 93.34% 



		
	
