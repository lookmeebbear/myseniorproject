# Satellite Derived Bathymetry with IceSAT-2 LiDAR Data : Case Study in the coast of Thailand
การศึกษาการทำแบบจำลองความลึกท้องน้ำตื้น (SATELLITE DERIVED BATHYMETRY) โดยใช้ภาพถ่ายดาวเทียมและค่าระดับจากไลดาร์บนดาวเทียม กรณีศึกษาพื้นที่ชายฝั่งทะเลประเทศไทย 
โครงงานทางวิศวกรรมประจำปีการศึกษา 2564 ของนายเทพชัย ศรีน้อย และ รศ.ดร.ไพศาล สันติธรรมนนท์ ภาควิชาวิศวกรรมสำรวจ คณะวิศวกรรมศาสตร์ จุฬาลงกรณ์มหาวิทยาลัย 


![Screenshot (419)](https://user-images.githubusercontent.com/88705136/171320963-0ac44fd4-2d7f-4b20-82e5-cd66bb4cf946.png)

ศึกษาการทำแบบจำลองความลึกท้องน้ำตื้น (Bathymetry Model) บริเวณชายฝั่งทะเลประเทศไทย จากภาพถ่ายดาวเทียม Sentinel-2 และค่าระดับจากระบบไลดาร์บนดาวเทียม ICESat-2 ผ่านการเขียน python programming จัดการข้อมูลและทำแบบจำลอง โดยนำเข้าข้อมูลภาพถ่ายจากระบบ Google Earth Engine

ความลึกตัวอย่างทำได้จากการคัดเลือกค่าระดับท้องน้ำและผิวน้ำจาก point cloud จาก ATLAS LiDAR บนดาวเทียม ICESat-2 นำข้อมูลดิบมานำเข้า pandas dataframe หากโหลดข้อมูลเริ่มต้นแบบ hdf5 file นำเข้า python ด้วย library h5py แล้วนำเข้า dataframe เพื่อความสะดวกในการจัดการ

ประเด็นที่สนใจคือเรื่องอัลกอริทึมทำแบบจำลอง (Stumpf or Lyzenga Algorithm) กับ แนวทางการตรวจแก้ภาพ (Sun Glint or Dark Object Subtraction Atmospheric Correction) ในพื้นที่ศึกษาหาดเจ้าสำราญ จังหวัดเพชรบุรี หาดท้ายเหมือง จังหวัดพังงา และเกาะหมาก จังหวัดตราด

ผลเบื้องต้นนั้น Lyzenga Algorithm มีความเหมาะสมกับพื้นที่แรก กับ Stumpf Algorithm มีความเหมาะสมกับสองพื้นที่หลัง โดยการเลือกภาพแบบไม่ต้องตรวจแก้ให้ผลลัผธ์ที่ดีกว่า ดังนั้นควรเลือกภาพให้ดีตั้งแต่เริ่มต้น นำเข้าทำแบบจำลองได้เลย ความถูกต้องอยู่ในระดับ 1 ถึง 3 เมตร

การศึกษานี้ยังมีประเด็นที่สามารถศึกษาต่อได้มากมาย ทั้งเรื่องการลด bias ของการวิจัย การเลี่ยง manual selection การตรวจแก้ภาพและค่าระดับให้ดีขึ้นพร้อมต่อการทำแบบจำลอง รูปแบบอัลกอริทึมที่เข้ากับธรรมชาติได้ดีกว่าสองอัลกอริทึมที่นำมาวิจัย

งานวิจัยนี้นำไปประยุกต์ใช้เป็นส่วนหนึ่งของการทำแผนที่เร่งด่วนสนับสนุนการฝึกช่วยเหลือผู้ประสบภัยทางทะเล 2565 (Rapid Mapping for HADR Exercise from the Sea 2022) นำเสนอโดย รองศาสตราจารย์ ดร. ไพศาล สันติธรรมนนท์ และคณะ โดยได้นำเสนอรายละเอียดเกี่ยวกับแผนที่เส้นชั้นความลึกท้องน้ำ SDB (Bathymetric Iso-depth from SDB) ดังนี้

โดยแผนที่เส้นชั้นความลึกท้องน้ำโดยปกติจะได้ผ่านการสำรวจโดยใช้คลื่นเสียงสะท้อนหยั่งความลึกน้ำแล้วผลิตแผนที่ความลึกท้องน้ำ เครื่องมือดังกล่าวเรียกว่า Echo Sounder ซึ่งจะต้องติดเรือที่มีคนขับหรือใช้เรือไร้คนขับ (Unmanned Vessel Survey : USV) ก็ได้ผลดีในปัจจุบัน อีกทางเลือกหนึ่ง ในปัจจุบันมีเทคนิคการผลิตแผนที่ความลึกน้ำตื้น (จำกัดความลึกที่ประมาณ <30 เมตร) ด้วยข้อมูลดาวเทียม เช่น LandSat8, LandSat9, Sentinel-2A และ Sentinel-2B ซึ่งเป็นข้อมูลฟรีและมีอัพเดทต่อเนื่องบนพื้นที่ใดๆบนโลก บ่อยซ้ำๆถึง 2.3 วัน (Li and Chen, 2020) พร้อมให้ดาวน์โหลดได้สะดวกเรียกใช้ทันทีผ่าน Google Earth Engine โดยอาศัยหลักการสะท้อนภาพความลึกท้องน้ำปรากฏบนข้อมูลภาพดาวเทียมสเปกตรัมต่าง ๆ มีผลตอบสนองที่แตกต่างกัน โดยการศึกษาหาความสัมพันธ์บางช่วงคลื่นของภาพดาวเทียมมัลติสเปคตรัม และความเข้าใจของฟิสิกส์การสะท้อนและดูดซับช่วงคลื่นแสงอาทิตย์ ทำให้มีงานวิจัยจำนวนมากในช่วงสัก 5 ปีที่ผ่านมาพิสูจน์ให้เห็นว่าเราสามารถใช้ข้อมูลภาพดาวเทียมมัลติสเปคตรัมหาความลึกท้องน้ำตื้นได้ การประมวลความลึกท้องน้ำแบบนี้เรียกว่า Satellite-Derived Bathymetry (SDB) สามารถนำไปผลิตแผนที่ความลึก น้ำตื้น (<30 เมตร) บริเวณชายฝั่งและแหล่งน้ำในแผ่นดินทั่วไปประเทศไทย ได้ แต่อย่างไรก็ตามความละเอียดถูกต้องของความลึกน้ำตื้นยังจำกัดอยู่ที่ +/- 1-3 เมตร และจะดีขึ้นมากหากมีข้อมูลในพื้นที่ (in-situ) มาช่วยการจำลองแบบ

ในการฝึกครั้งนี้ ในพื้นที่ชายฝั่งของจังหวัดระยองและจังหวัดตลอดแนวยาวจากนิคมอุตสาหกรรมมาบตาพุด จังหวัดระยอง ไปจนถึง อ่าวคุ้งกระเบน จังหวัดจันทบุรี ระยะทางรวมกว่า 122 กิโลเมตร และพื้นที่ชายฝั่งต่อเนื่องไปยังเกาะเสม็ดนั้น  พบว่าระดับความลึกน้ำตื้นเพียง 5-10 เมตร จึงทำให้การผลิตแผนที่ความลึกท้องน้ำทะเลทำได้อย่างมีประสิทธิภาพและสามารถทำได้ในเวลาน้อยกว่าชั่วโมงเท่านั้น แผนที่กริดความลึกน้ำตลอดแนวชายฝั่งประสบภัยได้รับผลกระทบจากพายุซัดชายฝั่ง แสดงในภาพ

![image](https://user-images.githubusercontent.com/88705136/213903731-28df2d20-a1c8-4541-9c99-0d9091e3bae0.png)

กริดของแผนที่ความลึกท้องน้ำ (Bathymetric Grid) ที่ผลิตจากภาพดาวเทียม Sentinel 1A/1B ความละเอียดจุดภาพ GSD เป็น 10 เมตร จะนำมาผลิตเป็นแผนที่เส้นชั้นความลึกท้องน้ำชนิดเวกเตอร์ เส้นชั้นความสูงชั้นละ 1 เมตรและ 5 เมตร เป็นข้อมูลเวกเตอร์ชนิดไฟล์ GeoPackage บางส่วนของพื้นที่เกาะเสม็ดแสดงดังภาพ 

![image](https://user-images.githubusercontent.com/88705136/213903746-c47260bf-9e9c-4066-beff-51fe8c465e8f.png)

กรมอุทกศาสตร์ กองทัพเรือมีภารกิจประจำในการสำรวจโดยใช้คลื่นเสียงสะท้อนหยั่งความลึกน้ำแล้วผลิตแผนที่ความลึกท้องทะเล ซึ่งอาจมีความละเอียดถูกต้องสูงกว่านี้มากตามมาตราฐานการหยั่งความลึกน้ำของ International Hydrographic Organization (S44 IHO- “Accuracy Standards Recommended for Hydrographic Surveys”) และเป็นเทคนิควิธีการมาตรฐานปัจจุบัน แต่อาจมีข้อจำกัดในวงรอบของการปรับปรุงแผนที่ความลึกท้องทะเลที่มีพื้นที่กว้างขวางมากทั้งอ่าวไทยและฝั่งทะเลอันดามัน นอกจากนี้เทคนิคการใช้เรือสำรวจใช้คลื่นเสียงสะท้อนหยั่งความลึกน้ำอาจมีข้อจำกัดในพื้นที่น้ำตื้นที่เรือกินน้ำลึกเข้าไม่ถึงหรือยากต่อการเข้าถึง ทั้งนี้ตลอดจนบริเวณชายฝั่งมักมีโขดหิน ป่าชายเลน สิ่งปลูกสร้าง ฟาร์มทะเลและข้อจำกัดในการเดินเรือสำรวจต่างๆ มากมาย ดังนั้นในภารกิจบรรเทาสาธารณภัย “from the Sea” ยังมีข้อมูลทางเลือก  SDB  ให้ใช้งานได้


ปัจจุบันนี้ เทพชัย ศรีน้อย กำลังเป็นนิสิตระดับปริญญาโท ภาควิชาวิศวกรรมสำรวจ คณะวิศวกรรมสำรวจ จุฬาลงกรณ์มหาวิทยาลัย มีความสนใจในงานวิจัยทางด้าน Remote Sensing สำหรับสิ่งแวดล้อมทางกายภาพ ทั้งด้านแหล่งน้ำ เมือง การใช้ประโยชน์ที่ดินและสิ่งปกคลุมดิน วิทยาศาสตร์โลก นอกจากนี้ยังสนใจเรื่อง Geodesy และ Cartography ด้วย 
ช่องทางติดต่อเจ้าของผลงาน thepchaisrinoi@gmail.com
