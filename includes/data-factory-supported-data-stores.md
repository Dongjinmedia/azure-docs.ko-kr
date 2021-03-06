데이터 팩터리의 복사 활동은 원본 데이터 저장소의 데이터를 싱크 데이터 저장소로 복사합니다. Data Factory는 다음과 같은 데이터 저장소를 지원합니다. 모든 소스의 데이터를 모든 싱크에 쓸 수 있습니다. 데이터 저장소를 클릭하면 해당 저장소에서/저장소로 데이터를 복사하는 방법을 확인할 수 있습니다.

| Category | 데이터 저장소 | 소스로 지원 | 싱크로 지원 |
|:--- |:--- |:--- |:--- |
| Azure |[Azure Blob 저장소](../articles/data-factory/data-factory-azure-blob-connector.md) <br/> [Azure Data Lake Store](../articles/data-factory/data-factory-azure-datalake-connector.md) <br/> [Azure SQL Database](../articles/data-factory/data-factory-azure-sql-connector.md) <br/> [Azure SQL Data Warehouse](../articles/data-factory/data-factory-azure-sql-data-warehouse-connector.md) <br/> [Azure Table Storage](../articles/data-factory/data-factory-azure-table-connector.md) <br/> [Azure DocumentDB](../articles/data-factory/data-factory-azure-documentdb-connector.md) <br/> [Azure Search 인덱스](../articles/data-factory/data-factory-azure-search-connector.md)|✓ <br/> ✓  <br/> ✓  <br/> ✓  <br/> ✓  <br/> ✓  |✓  <br/> ✓  <br/> ✓  <br/> ✓  <br/> ✓  <br/> ✓  <br/> ✓ |
| 데이터베이스 |[SQL Server](../articles/data-factory/data-factory-sqlserver-connector.md)\* <br/> [Oracle](../articles/data-factory/data-factory-onprem-oracle-connector.md)\* <br/> [MySQL](../articles/data-factory/data-factory-onprem-mysql-connector.md)\* <br/> [DB2](../articles/data-factory/data-factory-onprem-db2-connector.md)\* <br/> [Teradata](../articles/data-factory/data-factory-onprem-teradata-connector.md)\* <br/> [PostgreSQL](../articles/data-factory/data-factory-onprem-postgresql-connector.md)\* <br/> [Sybase](../articles/data-factory/data-factory-onprem-sybase-connector.md)\* <br/>[Cassandra](../articles/data-factory/data-factory-onprem-cassandra-connector.md)\* <br/>[MongoDB](../articles/data-factory/data-factory-on-premises-mongodb-connector.md)\*<br/>[Amazon Redshift](../articles/data-factory/data-factory-amazon-redshift-connector.md) |✓  <br/> ✓  <br/> ✓  <br/> ✓  <br/> ✓  <br/> ✓ <br/> ✓  <br/> ✓  <br/> ✓  <br/> ✓  |✓  <br/> ✓  <br/> &nbsp; <br/> &nbsp; <br/> &nbsp; <br/> &nbsp;<br/> &nbsp;<br/> &nbsp;<br/> &nbsp; <br/>&nbsp; |
| 파일 |[파일 시스템](../articles/data-factory/data-factory-onprem-file-system-connector.md)\* <br/> [HDFS](../articles/data-factory/data-factory-hdfs-connector.md)\* <br/> [Amazon S3](../articles/data-factory/data-factory-amazon-simple-storage-service-connector.md) <br/> [FTP](../articles/data-factory/data-factory-ftp-connector.md) |✓ <br/> ✓  <br/> ✓  <br/> ✓  |✓  <br/> &nbsp;<br/>&nbsp; |
| 기타 |[Salesforce](../articles/data-factory/data-factory-salesforce-connector.md)<br/> [일반 ODBC](../articles/data-factory/data-factory-odbc-connector.md)\* <br/> [일반 OData](../articles/data-factory/data-factory-odata-connector.md) <br/> [웹 테이블(HTML의 테이블)](../articles/data-factory/data-factory-web-table-connector.md) <br/> [GE Historian](../articles/data-factory/data-factory-odbc-connector.md#ge-historian-store)* |✓ <br/> ✓  <br/> ✓  <br/> ✓  <br/> ✓  |&nbsp; <br/> &nbsp; <br/> &nbsp; <br/> &nbsp;<br/> &nbsp;<br/> &nbsp; |

> [!NOTE]
> *가 있는 데이터 저장소는 온-프레미스 또는 Azure IaaS에 있을 수 있으며 온-프레미스/Azure IaaS 컴퓨터에 [데이터 관리 게이트웨이](../articles/data-factory/data-factory-data-management-gateway.md) 를 설치해야 합니다.
> 
> 



<!--HONumber=Nov16_HO2-->


