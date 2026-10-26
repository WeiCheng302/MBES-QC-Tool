MBES QC 專案範本

用途
- 「測量成果檢核」從點雲計算 Coverage、Density、STD，輸出 1 m DEM、Density、STD 及檢核報告。
- 「廠商交付成果檢核」比對廠商 DEM、Density、STD，並依 TVU、THU 門檻檢核不確定度；共同 QC 需五項在同一像元皆合格。

快速開始
1. 複製整個 MBES_QC_TEMPLATE 資料夾，作為本次專案資料夾。
2. 將點雲（XYZ、LAS 或 LAZ）放入 input\pointcloud。不要同時放入同一批資料的 XYZ 和 LAS 副本。
3. 將目標範圍 SHP 及同名 .shx、.dbf、.prj 等伴隨檔放入 input\boundary，預設檔名 survey_area.shp。
4. 將廠商 DEM、Density、STD、TVU、THU TIFF 放入 input\vendor_products，預設檔名分別為 DEM.tif、Density.tif、STD.tif、TVU.tif、THU.tif。
5. 在 mbes_tool\config.bat 設定 RUN_SURVEY_QC、RUN_DELIVERABLE_QC、業主/廠商名稱、門檻及 Python EXE。
6. XYZ 欄位順序為北距、東距、高程時，將 XYZ_AXIS_ORDER 設為 NEH；東距、北距、高程則設為 ENH。LAS/LAZ 依標準 X/Y/Z 讀取。
7. 執行專案根目錄的 run.bat。

資料夾用途
- input\pointcloud：本次點雲。
- input\boundary：目標 SHP 與必要的伴隨檔。
- input\vendor_products：廠商交付 TIFF。
- input\survey_qc_products：單獨執行「廠商交付成果檢核」時，放入既有測量成果檢核輸出的 DEM1M.tif、PointDensity1M.tif、STD1M.tif。
- output：報告、QC TIFF、差異 TIFF 與五項共同合規 TIFF。
- temp：程式暫存格網。
- mbes_tool：正式程式與設定。

流程設定
- 兩個流程都跑：RUN_SURVEY_QC=1、RUN_DELIVERABLE_QC=1；交付成果檢核自動使用本次點雲計算結果。
- 只跑測量成果檢核：RUN_SURVEY_QC=1、RUN_DELIVERABLE_QC=0。
- 只跑廠商交付成果檢核：RUN_SURVEY_QC=0、RUN_DELIVERABLE_QC=1；須先將既有 DEM、Density、STD 放入 input\survey_qc_products。

Config 路徑皆相對於專案根目錄；run.bat 會先切換到該目錄，複製範本後不必重設資料夾路徑。兩個流程內的檢查項目固定全開。

固定空間規格：EPSG:3826、1 m、NoData=-9999。TVU 預設採 IHO S-44 Edition 6.2.0 Special Order 公式；THU 預設 2 m。請依契約設定並確認廠商不確定度 TIFF 的單位與信賴水準。
