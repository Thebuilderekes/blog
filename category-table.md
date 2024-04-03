
## create category table

1 row -> id, type - INT, length - 11, default-none, attributes- unsigned, index- primary
2 row -> title, type - VARCHAR, length - 50
3 row -> description, type - TEXT, length - 50

THEN SAVE.

 
`<form action = "<?= ROOT_URL ?> admin/add-category-logic.php" enctype="multipart/form-data" method = "POST">`
on  the form in the `add-category.php` page