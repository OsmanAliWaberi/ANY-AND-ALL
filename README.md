# ANY-AND-ALL

## Merhabalar

Aşağıdaki sorgu senaryolarını **dvdrental** örnek veri tabanı üzerinden gerçekleştiriniz.



1. film tablosunda film uzunluğu length sütununda gösterilmektedir. Uzunluğu ortalama film uzunluğundan fazla kaç tane film vardır?


2. film tablosunda en yüksek rental_rate değerine sahip kaç tane film vardır?


3. film tablosunda en düşük rental_rate ve en düşün replacement_cost değerlerine sahip filmleri sıralayınız.


4. payment tablosunda en fazla sayıda alışveriş yapan müşterileri(customer) sıralayınız.


## Cevaplar :


1. 
```sql


select count(length) from film where length > (select avg(length) from film)


```


2. 
```sql


select count(*) from film where rental_rate = (select max(rental_rate) from film)


```


3. 
```sql


select count(*) from film 
where film_id = any 
(select film_id from film 
where rental_rate = (select min(rental_rate) from film) and 
replacement_cost = (select max(replacement_cost)from film)) 


```


4. 
```sql


select customer_id, count(customer_id)  from payment 
group by customer_id
order by count(customer_id) desc


```