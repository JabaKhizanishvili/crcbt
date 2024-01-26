
import csv
import time

def deduplicate_records(input_file, output_file):
    start_time = time.time()

    with open(input_file, 'r') as file:
        csv_reader = csv.reader(file)
        records = list(csv_reader)

    seen_records = set()
    deduplicated_records = []

    for record in records:
        key = tuple(record)
        if key not in seen_records:
            deduplicated_records.append(record)
            seen_records.add(key)

    with open(output_file, 'w', newline='') as file:
        csv_writer = csv.writer(file)
        csv_writer.writerows(deduplicated_records)

    end_time = time.time()

    execution_time = end_time - start_time
    print(f"process completed in {execution_time:.2f} seconds.")

input_csv_path = './file.csv'
output_csv_path = 'C:/Users/Jaba/Desktop/output_file.csv'


deduplicate_records(input_csv_path, output_csv_path)







--1



SELECT

    g.Name AS Genre,

    SUM(il.UnitPrice) AS TotalSales

FROM

    Genre g

JOIN

    Track t ON g.GenreId = t.GenreId

JOIN

    InvoiceLine il ON t.TrackId = il.TrackId

GROUP BY

    g.Name

ORDER BY

    TotalSales DESC

LIMIT 3;









--2



SELECT

    e.FirstName || ' ' || e.LastName AS EmployeeName,

    SUM(i.Total) AS TotalSales

FROM

    Employee e

LEFT JOIN

    Customer c ON e.EmployeeId = c.SupportRepId

LEFT JOIN

    Invoice i ON c.CustomerId = i.CustomerId

GROUP BY

    e.FirstName, e.LastName

ORDER BY

    TotalSales DESC;

   

   

   

--3



SELECT

    p.Name AS Playlist,

    COUNT(pt.TrackId) AS NumberOfTracks

FROM

    Playlist p

JOIN

    PlaylistTrack pt ON p.PlaylistId = pt.PlaylistId

GROUP BY

    p.Name

ORDER BY

    NumberOfTracks DESC

LIMIT 5;





   

   

--4



SELECT

    c.FirstName || ' ' || c.LastName AS CustomerName,

    COUNT(i.InvoiceId) AS TotalPurchases

FROM

    Customer c 

LEFT JOIN

    Invoice i ON c.CustomerId = i.CustomerId

GROUP BY

    c.FirstName, c.LastName

ORDER BY

    TotalPurchases DESC;


