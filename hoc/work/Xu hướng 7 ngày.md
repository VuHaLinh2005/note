SELECT  TOP 10
    pp.product_id,
    p.title,
    SUM(pp.quantity) AS total_quantity_sold
FROM 
    Purchased_Product pp
JOIN 
    Product p ON pp.product_id = p.id
JOIN 
    Invoice i ON pp.invoice_id = i.id
WHERE 
    i.created_at >= DATEADD(day, -7, GETDATE())
    AND i.created_at <= GETDATE()
    AND i.payment_status = 'Paid'
GROUP BY 
    pp.product_id, p.title
ORDER BY 
    total_quantity_sold DESC



