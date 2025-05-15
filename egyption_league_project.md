| p_id      | p_name      |
|-----------|-------------|
| 1         | Al Ahly     |
| 2         | Zamalek     |
| 3         | Pyramids    |



| m_id | p1_id        | p2_id        | p1_score | p2_score |
|------|--------------|--------------|----------|----------|
| 1    | 1 (Al Ahly)  | 2 (Zamalek)  | 3        | 3        |
| 2    | 1 (Al Ahly)  | 3 (Pyramids) | 2        | 1        |
| 3    | 2 (Zamalek)  | 3 (Pyramids) | 3        | 0        |
| 2    | 3 (Pyramids) | 2 (Zamalek)  | 3        | 2        |



``` sql

create database egyption_league;
Go

use egyption_league;
Go

create table players(
	id int,
	p_name varchar(30)
);
create table matches(
	m_id int not null,
	p1_id int,
	p2_id int,
	p1_score int,
	p2_score int
);
-- change the name of table players to clubs
EXEC sp_rename 'players', 'clubs';

-- change name of players id to p_id
EXEC sp_rename 'players.id', 'p_id','column';

-- change p_id to be not null to be a primary key
alter table clubs
alter column p_id int not null; 

-- change p_id to primary key
alter table clubs
add constraint p_id_pk primary key (p_id);

-- modification on matches table
-- change p1_id , p2_id , p1_score , p2_score to not null
alter table matches 
alter column p1_id int not null;

alter table matches 
alter column p2_id int not null;

alter table matches 
alter column p1_score int not null;

alter table matches 
alter column p2_score int not null;
	  
-- change constraint of scores to be >= 0
alter table matches 
add constraint p1_score_chk check (p1_score >= 0);

alter table matches 
add constraint p2_score_chk check (p2_score >= 0);

-- connect the two table via foreign key

alter table matches
add constraint p1_id_fk foreign key (p1_id)
references clubs (p_id);

alter table matches
add constraint p2_id_fk foreign key (p2_id)
references clubs (p_id);

-- case p1_id != p2_id 

alter table matches
add check (p1_id != p2_id);

-- insertion

insert into clubs(p_id,p_name)
values (1,'Al Ahly'),
	  (2,'Zamalek'),
	  (3,'Pyramids');


insert into matches(m_id,p1_id,p2_id,p1_score,p2_score)
values (1,1,2,3,3),
	  (2,1,3,2,1),
	  (3,2,3,3,0),
	  (2,3,2,3,2);

```
