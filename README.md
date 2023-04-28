# ML-Classification_AS1
Project Firewall database

1. Get data from log file link https://www.kaggle.com/datasets/tunguz/internet-firewall-data-set

	Fatih Ertam (2023) ได้วิเคราะห์ข้อมูลการบันทึกบนอุปกรณ์ไฟร์วอลล์และควบคุมการรับส่งข้อมูลทางอินเทอร์เน็ตตามผลการวิเคราะห์ที่มาจากการบันทึกการใช้อุปกรณ์ไฟร์วอลล์ของ Firat University ซึ่งจำแนกข้อมูลออกเป็น 4 คลาสโดยใช้วิธี SVM ได้แก่ Linear, Polynomial, Sigmoid และ RBF เพื่อให้ได้ผลลัพธ์ที่ดีที่สุดสำหรับการศึกษานี้ ประสิทธิภาพของตัวแยกประเภทได้รับการประเมินโดยใช้ความไว การเรียกคืน และ ค่าเฉลี่ยฮาร์มอนิกของคะแนน F1 เราสามารถระบุได้ว่าข้อมูลที่สร้างขึ้นจากการจัดหมวดหมู่มีความเกี่ยวข้องกับข้อมูลที่ตั้งใจไว้มากน้อยเพียงใด ในการศึกษานี้ ใช้ 11 ลักษณะ ในการวิเคราะห์เหตุการณ์ 65,532 ครั้ง ตามตาราง 
	
	![Screenshot 2023-04-28 213846](https://user-images.githubusercontent.com/122291438/235178139-78356fc9-1c01-4ac2-80aa-adf48f618edf.png)


SVM ที่เลือกฟังก์ชันการเปิดใช้งาน Sigmoid 98.5% ให้ค่าการเรียกคืนสูงสุด ในขณะที่ตัวแยกประเภท SVM ที่มีฟังก์ชันการเปิดใช้งานเชิง Linear 67.5% ให้ค่าความแม่นยำสูงสุด ตามค่าคะแนน F1 พบว่าลักษณนามที่ใช้การเปิดใช้งาน 76.4% RBF นั้นให้ผลลัพธ์มากที่สุด เมื่อใช้ฟังก์ชันกระตุ้น Polynomial ในการจำแนกข้อมูล พบว่าทั้งค่าความแม่นยำและค่าการเรียกคืนอยู่ในระดับต่ำ เมื่อคำนึงถึงค่าเฉลี่ย จะเห็นได้ชัดว่าตัวแยกประเภทตามฟังก์ชันการเปิดใช้งาน RBF นั้นดีที่สุด สำหรับแต่ละคลาส เส้นโค้งลักษณะการทำงานของเครื่องรับ (ROC) ก็ถูกสร้างขึ้นเช่นกัน ดังนั้นจึงมีการนำเสนอการเปรียบเทียบด้วยภาพของอัตราบวกจริงและอัตราบวกปลอม การออกแบบระบบอัจฉริยะที่สามารถเลือกจัดการ ข้อมูลได้มากขึ้นด้วยตัวมันเอง โครงสร้างพื้นฐานที่จำเป็นเพื่อให้บรรลุเป้าหมายสุดท้ายได้ถูกสร้างขึ้นผ่านกิจกรรมนี้ การตรวจสอบในอนาคตอาจให้ผลลัพธ์ที่เป็นประโยชน์เนื่องจากระบบที่เตรียมไว้มีความแม่นยำสูง  (Table III.)
	![Screenshot 2023-04-28 214448](https://user-images.githubusercontent.com/122291438/235179021-07bb4b52-393c-4d03-bcd3-7ae82aafc8d7.png)

	ข้อจำกัดในงานวิจัยนี้คือ SVM ใช้เพื่อแยกสองคลาส แต่อาจใช้เพื่อจัดการปัญหาที่เกี่ยวข้องกับสองคลาสขึ้นไป ไม่เหมาะกับการใช้กับข้อมูลที่มีความสูงต่ำกว่า data point จึงต้องแปลงข้อมูลให้อยู่ใน input space ไปสู่ transformed Space ที่เรียกว่า Feature space จึงสามารถใช้ตัวแบบ SVM ได้ในการแบ่ง ข้อมูลด้วย Hyperplane เช่น Polynomial Kernel, Radial Basis Function(RBF), Sigmoid Kernel 

2. ทำการ Collect data และ inpectation data
3. ทำ Data Exploration ( EDA ) 

		3.1 จำนวนActionที่เกิดขึ้นในtransaction
		
<img width="1000" alt="ภาพถ่ายหน้าจอ 2566-04-28 เวลา 20 40 34" src="https://user-images.githubusercontent.com/127765032/235164910-e0f082c4-f042-4aeb-b368-aed89fd65dd6.png">
		
		3.2 การหาค่าmeanของ Elapsed time (sec)

<img width="1000" alt="ภาพถ่ายหน้าจอ 2566-04-28 เวลา 20 40 45" src="https://user-images.githubusercontent.com/127765032/235164916-79592a7a-f093-4f59-b899-5e02bccd2ef8.png">

		3.3 การหาค่า meanของ Bytes

<img width="1000" alt="ภาพถ่ายหน้าจอ 2566-04-28 เวลา 20 40 58" src="https://user-images.githubusercontent.com/127765032/235164925-3aad5a00-bcb3-4344-8aa0-b0588d5bc8a9.png">
		
		
		3.4 การหา correlation ของ Bytes & time แบบไม่ได้ remove bytes ที่เป็นoutliner ออก
		3.5 การหา correlation ของ Bytes & time แบบปรับค่า น้อยกว่าเท่ากับ 1000
		3.6 การหา correlation ของ Bytes & time แบบปรับค่า น้อยกว่าเท่ากับ 10000
		3.7 การหา correlation ของ Bytes & time แบบปรับค่า น้อยกว่าเท่ากับ 100000
	
		


<img width="1000" alt="ภาพถ่ายหน้าจอ 2566-04-28 เวลา 20 24 38" src="https://user-images.githubusercontent.com/127765032/235159698-0f0a7407-7860-46f7-a641-0cc8bc192049.png">

		3.8 การหา Top Destionation port ที่มีการเกิดtransactionมากที่สุด
		3.9 การหา Top Source port ที่มีการเกิดtransactionมากที่สุด
		
		
<img width="1000" alt="ภาพถ่ายหน้าจอ 2566-04-28 เวลา 20 30 17" src="https://user-images.githubusercontent.com/127765032/235161200-675e846d-fd93-4892-aab1-c7ee69c39089.png">



		3.10 การหา Correlation heatmap เพื่อดูความสัมพันธ์ของFeature ทุกตัว
		
<img width="1000" alt="ภาพถ่ายหน้าจอ 2566-04-28 เวลา 21 19 43" src="https://user-images.githubusercontent.com/127765032/235173429-5b1c5752-d22a-4f45-8c87-b2ed970c338f.png">		
		

4. Traning Model Tools

		4.1 Cart Method
		
		
<img width="1000" alt="ภาพถ่ายหน้าจอ 2566-04-28 เวลา 21 02 51" src="https://user-images.githubusercontent.com/127765032/235169339-deee6f76-2974-409d-a072-1710a4969754.png">		
	
		4.2 Random Forest
<img width="1000" alt="ภาพถ่ายหน้าจอ 2566-04-28 เวลา 21 35 35" src="https://user-images.githubusercontent.com/127765032/235177026-efdc781c-b692-4e41-877b-c1edb8d7d9ef.png">
	
	
	
	
	
		4.3 XGBoot
		4.4 K-NN
		4.5 Support Vector Machine 
		

5. Test
		5.1 แบ่ง Train 70%  Test 30%
		5.2 แบ่ง Train 80%  Test 20%
		5.3 แบ่ง Train 90%  Test 10%
	
6.Evaluation

		6.1 F1 Score เทียบผล
![Screenshot 2023-04-28 205757](https://user-images.githubusercontent.com/122291438/235169008-9e32d34a-96b7-4ae5-a718-8c0f09ebd5be.png)

สรุปผล: จากการทดลอง จะเห็นได้อย่างชัดเจนค่าของ F1 score ของ Randome Forest มาหที่สุด = 99.77% ในขณะที่ Model อื่นAvgate อยู่ที่ 99.63% bha bha bha 
show ROC หรือ chart ธรรมดา



7.ใช้model สามารถที่จะimprove number ได้เป็น....% 

https://user-images.githubusercontent.com/127765032/234913998-0fc9f0b7-fd61-4f3d-aa74-08ade6f84eec.png



		
	
