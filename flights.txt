flight(ac987,airCanada,toronto,montreal). % 1
flight(ac231,airCanada,toronto,losAngeles). % 2
flight(ac633,airCanada,toronto,losAngeles).
flight(ua333,unitedAirlines,chicago,toronto). % 3
flight(aa721,americanAirlines,ny,london). % 4
flight(ac562,airCanada,edmonton,montreal). % 5
flight(ac888,airCanada,toronto,vancouver). % 6
flight(ac802,airCanada,vancouver,shanghai). % 7
flight(ac222,airCanada,montreal,ny). % 8
flight(ac363,airCanada,toronto,shanghai). % 9
flight(ac463,airCanada,toronto,shanghai). % 10
flight(ac277,airCanada,toronto,edmonton). % 11
flight(ac835,airCanada,toronto,beijing). % 12
flight(ua123,unitedAirlines,montreal,chicago).
flight(ac998,airCanada,toronto,london). % 1
flight(ac999,airCanada,toronto,london). % 1
flight(ua199,unitedAirlines,ny,chicago).
flight(ua300,americanAirlines,ny,miami).

% MORNING IS BETWEEN 500 AND 900
% DAY IS BETWEEN 900 AND 1200
% AFTERNOON IS 1200 TO 1700
% EVENEING IS 1700 TO 2200
% NO FLIGHTS BETWEEN 2200 AND 500, 2300, 2400, 100, 200, 300, 400

dtime(ac987,toronto,900). % 530 hours AC987 ANSWER TO 11
dtime(ac231,toronto,815). % #1
dtime(ac633,toronto,1300). % ANSWER TO 6
dtime(ua333,chicago,1900).
dtime(aa721,ny,1300).
dtime(ac562,edmonton,1050).
dtime(ac888,toronto,530). % 770 hours 
dtime(ac802,vancouver,1200). % 950 hours - ANSWER TO 8
dtime(ac222,montreal,800).
dtime(ac363,toronto,630). %1370 hours
dtime(ac463,toronto,830). % 1300 hours 
dtime(ac277,toronto, 1115).
dtime(ac835,toronto,500).
dtime(ua123,montreal,200).
dtime(ac998,toronto,930). % ANSWER TO Q 3, 7
dtime(ac999,toronto,1130). % ANSWER TO Q 7
dtime(ua199,ny,1350).
dtime(ua300,ny,930).

atime(ac987,montreal,1430).
atime(ac231,losAngeles,1400).
atime(ac633,losAngeles,1500).
atime(ua333,toronto,2100).
atime(aa721,london,1530).
atime(ac562,montreal,1650).
atime(ac888,vancouver,1300).
atime(ac802,shanghai,2150).
atime(ac222,ny,1000).
atime(ac363,shanghai,2000).
atime(ac463,shanghai,2130).
atime(ac277,edmonton,1555).
atime(ac835,beijing,2130).
atime(ua123,chicago,900).
atime(ac998,london,2100).
atime(ac999,london,2100).
atime(ua199,chicago,1550).
atime(ua300,miami,1490).

location(toronto,canada).
location(montreal,canada).
location(edmonton,canada).
location(vancouver,canada).
location(losAngeles,us).
location(chicago,us).
location(ny,us).
location(london,uk).
location(beijing,china).
location(shanghai,china).
location(miami,us).

article(a). article(the). article(any). article(an).

common_noun(flight, X):- flight(X,Flight,Depart,City).
common_noun(city, X):- location(X,Y).
common_noun(country,X):- location(Z,X).
common_noun(time, X):- dtime(Flight,City,X).
common_noun(time,X):- atime(Flight,City,X).

proper_noun(toronto).
proper_noun(losAngeles).
proper_noun(canada).
proper_noun(uk).
proper_noun(london).
proper_noun(edmonton).
proper_noun(chicago).
proper_noun(us).
proper_noun(shanghai).
proper_noun(vancouver).
proper_noun(ny).
proper_noun(beijing).
proper_noun(china).
proper_noun(montreal).
proper_noun(miami).
proper_noun(luton).

adjective(domestic,X):- flight(X,Flight,City1,City2), location(City1,Y), location(City2,Y), not City1=City2.
adjective(international,X):- flight(X,Flight,City1,City2), location(City1,Y), location(City2,Z), not Y=Z.
adjective(airCanada,X):- flight(X,airCanada,City1,City2).
adjective(unitedAirlines,X):- flight(X,unitedAirlines,City1,City2).
adjective(americanAirlines,X):- flight(X,americanAirlines,City1,City2).
adjective(long,X) :- flight(X, Carrier, City, Destination), dtime(Flight, City, DTime), atime(Flight, Destination, ATime), Time is ATime - DTime, not (flight(Flight2, Carrier2, City, Destination), dtime(Flight2, City, DTime2), atime(Flight2, Destination, ATime2), Time2 is ATime2 - DTime2, Time2 > Time).
adjective(shortest,X) :- flight(X, Carrier, City, Destination), dtime(Flight, City, DTime), atime(Flight, Destination, ATime), Time1 is ATime - DTime, not (flight(Flight2, Carrier2, City, Destination), dtime(Flight2, City, DTime2), atime(Flight2, Destination, ATime2), Time2 is ATime2 - DTime2, Time2 < Time1).
adjective(departure,X) :- flight(Flight,Airline,City1,City2), dtime(Flight, City1, X).
adjective(arrival,X) :- flight(Flight,Airline,City1,City2), atime(Flight, City2, X).
adjective(morning,X):- dtime(X,City,DTime), DTime>459, DTime<900. % If you wanna return a FLIGHT in the morning/day/evening, MORNING IS BETWEEN 5AM AND 9AM
%adjective(morning,X):- atime(X,City,ATime), ATime>459, ATime<900.
adjective(day,X):- dtime(X,City,DTime), DTime>900, DTime<1200. % DAY IS BETWEEN 9AM AND NOON
%adjective(day,X):- atime(X,City,ATime), ATime>900, ATime<1200.
adjective(afternoon,X):- dtime(X,City,DTime), DTime>1200, DTime<1700. % AFTERNOON IS NOON TO 5PM
%adjective(afternoon,X):- atime(X,City,ATime), ATime>1200, ATime<1700.
adjective(evening,X):- dtime(X,City,DTime), DTime>1700, DTime<2200. % EVENEING IS 5PM TO 10PM
%adjective(evening,X):- atime(X,City,ATime), ATime>1700, ATime<2200.
adjective(morning,X):- dtime(Flight,City,X), X>459, X<901. % If you wanna return a TIME in the morning/day/evening
adjective(morning,X):- atime(Flight,City,X), X>459, X<901.
adjective(day,X):- dtime(Flight,City,X), X>900, X<1200.
adjective(day,X):- atime(Flight,City,X), X900, X<1200.
adjective(afternoon,X):- dtime(Flight,City,X), X>1200, X<1700.
adjective(afternoon,X):- atime(Flight,City,X), X>1200, X<1700.
adjective(evening,X):- dtime(Flight,City,X), X>1700, X<2200.
adjective(evening,X):- atime(Flight,City,X), X>1700, X<2200.
adjective(canadian,X):-flight(X,Airline,City1,City2), location(City1,canada).
adjective(canadian,X):-flight(X,Airline,City1,City2), location(City2,canada).
adjective(canadian,X):- location(X,canada).
adjective(chinese,X):-location(X,china).
adjective(chinese,X):-flight(X,Airline,City1,City2), location(City1,china).
adjective(chinese,X):-flight(X,Airline,City1,City2), location(City2,china).
adjective(american,X):-flight(X,Airline,City1,City2), location(City1,us).
adjective(american,X):-flight(X,Airline,City1,City2), location(City2,us).
adjective(american,X):-location(X,us).

preposition(to,X,Y):- flight(X,Airline,City1,Y). % flight X to city Y
preposition(to,X,Y):-location(Z,Y),flight(X,Airline,City,Z).
preposition(from,X,Y) :- flight(X,Carrier, Y, City).
preposition(from,X,Y):-location(Z,Y), flight(X,Airline,Z,City).
preposition(in,X,Y):-location(X,Y).
preposition(with,X,Y) :- dtime(X,City1,Y). % a flight X with departure time Y
preposition(with,X,Y) :- atime(X,City2,Y).
preposition(between,X,Y):-flight(X,Carrier, Y, City).
preposition(between,X,Y):-location(Z,Y), flight(X,Airline,Z,City).
preposition(and,X,Y):-flight(X,Airline,City1,Y).
preposition(and,X,Y):-location(Z,Y),flight(X,Airline,Z,City).
preposition(of,X,Y):- atime(Y,City,X).
preposition(of,X,Y):- dtime(Y,City,X).

% AMBIGUITY
preposition(to,X,Y):- flight(Y,Airline,City1,X). % flight X to city Y
preposition(to,X,Y):-location(Z,X),flight(Y,Airline,City,Z).
preposition(from,X,Y) :- flight(Y,Carrier, X, City).
preposition(from,X,Y):-location(Z,X), flight(Y,Airline,Z,City).


% PARSER

what(Words,Ref):- np(Words,Ref).
np([Location],Location) :- proper_noun(Location).
np([Art | Rest],What) :- article(Art), np2(Rest,What). 
np2([Adj | Rest], What) :- adjective(Adj,What), np2(Rest,What).
np2([Noun | Rest],What) :- common_noun(Noun,What), mods(Rest,What).
mods([],_).
mods(Words,What) :- append2(Start,End,Words), pp(Start,What), mods(End,What).
pp([Prep|Rest],What) :- preposition(Prep,What,What2), np(Rest,What2).

append2([],X,X).
append2([H|L1],L2,[H|Result]) :- append2(L1,L2,Result).




