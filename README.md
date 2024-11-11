# Supplier Data Access and Role-Based Privileges for Printer Products

## Overview
This script demonstrates how to create a view, define roles, and grant specific privileges to manage access to supplier data related to printer products. The script creates a view for suppliers with printer-related products and sets up roles with varying levels of access to different data columns, including restrictions on the `SupplierDiscount` column.

## SQL Steps

CREATE VIEW PrinterSupplierView AS
SELECT *
FROM Supplier
WHERE ProdName LIKE '%Printer%';

CREATE ROLE PrinterProductEmp;
CREATE ROLE PrinterProductMgr;
CREATE ROLE StoreMgr;

GRANT SELECT (SupplierID, SupplierName, SupplierAddress, SupplierPhone, SupplierEmail, ProdName)
ON PrinterSupplierView
TO PrinterProductEmp;

GRANT SELECT, UPDATE (SupplierID, SupplierName, SupplierAddress, SupplierPhone, SupplierEmail, ProdName)
ON PrinterSupplierView
TO PrinterProductMgr;

GRANT SELECT, INSERT, UPDATE (SupplierDiscount), DELETE
ON PrinterSupplierView
TO StoreMgr;

## Summary of Privileges
- **PrinterProductEmp**: Read-only access to all columns except `SupplierDiscount`.
- **PrinterProductMgr**: Read and modify access to all columns except `SupplierDiscount`.
- **StoreMgr**: Full access to all columns, including the ability to manage `SupplierDiscount`.
