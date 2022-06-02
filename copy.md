https://www.geeksforgeeks.org/docker-copy-instruction/?ref=lbp
This copies all files in the AccountingYearCategoryType directory to /etl/AccountingYearCategoryType

WORKDIR /etl/AccountingYearCategoryType
COPY ./AccountingYearCategoryType .

WORKDIR /etl/AccountingAccount
COPY ./AccountingAccount .