# adv_project1


```
set SQL_SAFE_UPDATES = 0;
update cleaned_file 
set 
    name = NULLIF(TRIM(name), ''),
    review_count = NULLIF(TRIM(review_count), ''),
    genre = NULLIF(TRIM(genre), ''),
    location = NULLIF(TRIM(location), ''),
    best_comment = NULLIF(TRIM(best_comment), '');
set SQL_SAFE_UPDATES = 1;
```

1-Get the top 5 highest-rated Cinema
```
select name, rating
from cleaned_file
where name is not null
order by rating desc
limit 5;
```
<img width="240" alt="1p" src="https://github.com/user-attachments/assets/3324406b-8332-4420-acb9-6495b9f649e1" />


2-Count the number of Cinema by genre
```
select genre, count(*) count
from cleaned_file
group by genre
order by count desc;
```
<img width="254" alt="412212506-3380c56d-032e-412f-b15f-f7e423e154ec" src="https://github.com/user-attachments/assets/439736ed-2416-4be0-96d3-e0a9fc190080" />


3-Find Cinema with missing best comments
```
select name,best_comment
from cleaned_file 
where best_comment is NULL;
```
<img width="262" alt="412212989-e2404042-0460-4cfb-b98d-729bc397aafd" src="https://github.com/user-attachments/assets/4cc90537-688f-4cad-8326-394ad7057231" />


4-List all Cinema in a specific city ("Dammam")
```
select name, location 
from cleaned_file
where location like '%Dammam%';
```
<img width="423" alt="412206534-7532a98c-3699-45a4-b19f-eb05e62fa490" src="https://github.com/user-attachments/assets/b76729c6-5bae-46b0-bbd1-43990b5e714a" />


5-Find the average rating for each genre
```
select genre, avg(rating) avg_rating
from cleaned_file
group by genre
order by avg_rating desc;
```
<img width="385" alt="412204321-1ceeea31-7752-4226-a6b6-d7377e73d1a0" src="https://github.com/user-attachments/assets/c81bd388-0744-4214-92fe-2c835fc8c6e8" />


6-Retrieve Cinema that have the word ‘Theater’ in their name
```
select name
from cleaned_file
where name like '%Theater%';
```
<img width="184" alt="412204946-57ce0b11-68b0-49bc-82b8-b2ac4f88a097" src="https://github.com/user-attachments/assets/30588373-e4a7-4e85-a1bf-4ae42ef931c7" />



7-.Count how many Cinema have a rating of 5
```
select count(*) Five_Star_Cinemas
from cleaned_file
where rating = 5;
```
<img width="121" alt="412205238-0363e235-157b-4982-b9a1-9ef6b56c2bbc" src="https://github.com/user-attachments/assets/40c87d44-4dac-41b0-bb04-4196dc2eb346" />



8-Find Cinema with the longest best comment
```
select name, length(best_comment) comment_length
from cleaned_file
where best_comment is not null
order by comment_length desc
limit 1;
```
<img width="276" alt="412205617-20713a37-64c4-47df-91a0-9aaee0c8bc57" src="https://github.com/user-attachments/assets/a5e64898-698e-4674-a530-eaf7509727a8" />



9-Get the highest-rated Cinema in each city
```
select name, location, rating Max_rating
from cleaned_file
where rating = (select max(rating) from cleaned_file);
```
<img width="493" alt="412219906-7980081f-a746-47aa-93b4-d1fa1465651a" src="https://github.com/user-attachments/assets/dcf19d8d-5bab-43a6-9965-f0c8f0a469b0" />



10-Find the Cinema with the most reviews ( Replaceing 000 to K )
```
select name, review_count 
from cleaned_file 
where name is not null
order by cast(replace(review_count, 'K', '000') as unsigned) desc;
```
<img width="265" alt="412221196-ffd1fb21-d499-46bd-bc64-8347ffc88399" src="https://github.com/user-attachments/assets/c20b5a45-da77-4783-8855-6db185593419" />

-Create a Function that returns Dammam's Data when selecting
```
delimiter //
create function get_location()
returns varchar(255)
deterministic
begin
    return 'Dammam\'s Data';
end //
delimiter ;
```
```
select name, rating, review_count, genre, get_location() location , best_comment
from cleaned_file
where best_comment is not null;
```
<img width="766" alt="412222872-c5de577d-f66f-4f9f-b1de-c619beb09c2a" src="https://github.com/user-attachments/assets/3055e1df-a88b-477b-9bee-f00d02041bef" />






