# ML-Classification_AS1
Project Firewall database

Firewall database จากข้อมูลข้างต้นที่ได้มาเป็น log file 12 columns 65532 rows ข้อมูล contain เป็น string และ numericโดยที่นำข้อมูลผ่านกระบวนดั้ง

1. Get data from log file link https://www.kaggle.com/datasets/tunguz/internet-firewall-data-set
2. ทำการ Collect data และ inpectation data
3. ทำ Data Exploration ( EDA ) 

		3.1 จำนวนActionที่เกิดขึ้นในtransaction
		3.2 การหาค่าmeanของ Elapsed time (sec)
		3.3 การหาค่า meanของ Bytes
		3.4 การหา correlation ของ Bytes & time แบบไม่ได้ remove bytes ที่เป็นoutliner ออก
		3.5 การหา correlation ของ Bytes & time แบบปรับค่า น้อยกว่าเท่ากับ 1000
		3.6 การหา correlation ของ Bytes & time แบบปรับค่า น้อยกว่าเท่ากับ 10000
		3.7 การหา correlation ของ Bytes & time แบบปรับค่า น้อยกว่าเท่ากับ 100000
		3.8 การหา Top Destionation port ที่มีการเกิดtransactionมากที่สุด
		3.9 การหา Top Source port ที่มีการเกิดtransactionมากที่สุด
		3.10 การหา Correlation heatmap เพื่อดูความสัมพันธ์ของFeature ทุกตัว


<img width="874" alt="ภาพถ่ายหน้าจอ 2566-04-28 เวลา 20 24 38" src="https://user-images.githubusercontent.com/127765032/235159698-0f0a7407-7860-46f7-a641-0cc8bc192049.png">


4. Traning Model Tools

		4.1 Cart Method
		4.2 Random Forest
		4.3 XGBoot
		4.4 K-NN
		4.5 Support Vector Machine 
		

5. Test
		5.1 แบ่ง Train 70%  Test 30%
		5.2 แบ่ง Train 80%  Test 20%
		5.3 แบ่ง Train 90%  Test 10%
	
6.Evaluation

		6.1 F1 Score เทียบผล
		

สรุปผล: จากการทดลอง จะเห็นได้อย่างชัดเจนค่าของ F1 score ของ Randome Forest มาหที่สุด = 99.77% ในขณะที่ Model อื่นAvgate อยู่ที่ 99.63% bha bha bha 
show ROC หรือ chart ธรรมดา



7.ใช้model สามารถที่จะimprove number ได้เป็น....% 

https://user-images.githubusercontent.com/127765032/234913998-0fc9f0b7-fd61-4f3d-aa74-08ade6f84eec.png



		
	
