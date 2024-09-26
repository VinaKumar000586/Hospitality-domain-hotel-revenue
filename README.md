![image alt]([image_url](https://github.com/VinaKumar000586/Hospitality-domain-hotel-revenue/blob/main/Hospitality%20Dashboard.png))


Revenue = SUM(fact_bookings[revenue_realized])
Total Bookings = COUNT(fact_bookings[booking_id])
Total Capacity = SUM(fact_aggregated_bookings[capacity])
Total Succesful Bookings = SUM(fact_aggregated_bookings[successful_bookings])
Occupancy % = DIVIDE([Total Succesful Bookings],[Total Capacity],0)
Average Rating = AVERAGE(fact_bookings[ratings_given])
No of days = DATEDIFF(MIN(dim_date[date]),MAX(dim_date[date]),DAY) +1
Total cancelled bookings = CALCULATE([Total Bookings],fact_bookings[booking_status]="Cancelled")
Cancellation % = DIVIDE([Total cancelled bookings],[Total Bookings])
Total Checked Out = CALCULATE([Total Bookings],fact_bookings[booking_status]="Checked Out")
Total no show bookings = CALCULATE([Total Bookings],fact_bookings[booking_status]="No Show")
No Show rate % = DIVIDE([Total no show bookings],[Total Bookings])
"Booking % by Platform = DIVIDE([Total Bookings],
 CALCULATE([Total Bookings], 
 ALL(fact_bookings[booking_platform])
  ))*100"
"Booking % by Room class = DIVIDE([Total Bookings],
 CALCULATE([Total Bookings], 
 ALL(dim_rooms[room_class])
  ))*100"
ADR = DIVIDE( [Revenue], [Total Bookings],0)
Realisation % = 1- ([Cancellation %]+[No Show rate %])
RevPAR = DIVIDE([Revenue],[Total Capacity])
DBRN = DIVIDE([Total Bookings], [No of days])
DSRN = DIVIDE([Total Capacity], [No of days])
DURN = DIVIDE([Total Checked Out],[No of days])
"Revenue WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([Revenue],dim_date[wn]= selv)
var revpw =  CALCULATE([Revenue],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

return


DIVIDE(revcw,revpw,0)-1"
"Occupancy WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([Occupancy %],dim_date[wn]= selv)
var revpw =  CALCULATE([Occupancy %],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

return


DIVIDE(revcw,revpw,0)-1"
"ADR WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([ADR],dim_date[wn]= selv)
var revpw =  CALCULATE([ADR],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

return


DIVIDE(revcw,revpw,0)-1"
"Revpar WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([RevPAR],dim_date[wn]= selv)
var revpw =  CALCULATE([RevPAR],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

return


DIVIDE(revcw,revpw,0)-1"
"Realisation WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([Realisation %],dim_date[wn]= selv)
var revpw =  CALCULATE([Realisation %],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

return


DIVIDE(revcw,revpw,0)-1"
"DSRN WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([DSRN],dim_date[wn]= selv)
var revpw =  CALCULATE([DSRN],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

return


DIVIDE(revcw,revpw,0)-1"


