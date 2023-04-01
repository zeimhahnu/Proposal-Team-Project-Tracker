# Proposal-Team-Project-Tracker
A google sheet dashboard to track the past and current on-going project handling by the proposal team in FootfallCam.
It comprises of multiple drop-down filters and able to filter out the "Date since Last Update" & "Planned next action date/ Deadline". 

Purposes of this dashboard 
1. To easily visualize the current projects handled by each person in the team, 
2. To determine each team member's bandwidth, 
3. To easily filter out and focus on the upcoming tight deadline/ high priority project during standup meeting between the team and manager.

The data and dashboard google drive URL: 
https://docs.google.com/spreadsheets/d/19NfqqyYNbH01P9dBhJ2wWUDEKfLPlkwLrprDJAhD6o8/edit?usp=share_link


<img src="Proposal Team Project Tracker Dashboard.png" width ="800">


Methodology

1. Write a google query function as shown below:

=QUERY('Company Proposal Tracker'!B1:T162,"
SELECT dateDiff(date'"&TEXT(A39,"yyyy-MM-dd")&"',G),T, P, C, D, E, G, H, J, L, M,N,O, Q
WHERE 
((O = '"&C40&"' AND NOT O = '') OR '"&C40&"' = 'All')
" & IF(I40<>"", "AND (S <= "&I40&" AND NOT S = '') ", "") & "
" & IF(I41<>"", "AND (T <= "&I41&" AND T IS NOT NULL) ", "") & "
" & IF(G44="Active", " AND (D = 'New' OR D = 'Ongoing Follow Up' OR D ='Sent Proposal')",
IF(G44="Inactive", " AND (D <> 'New'AND D <> 'Ongoing Follow Up'AND D <> 'Sent Proposal')", "")) & "
AND ((E = '"&C41&"' AND NOT E = '') OR '"&C41&"' = 'All')
AND ((P = '"&C42&"' AND NOT P = '') OR '"&C42&"' = 'All')
AND ((O = '"&F43&"' AND NOT O = '') OR '"&F43&"' = 'All')
AND ((J = '"&F42&"' AND NOT J = '') OR '"&F42&"' = 'All')
AND ((D = '"&F44&"' AND NOT D = '') OR '"&F44&"' = 'All')
AND ((L = '"&C43&"' AND NOT L = '') OR '"&C43&"' = 'All')
AND ((M = '"&C44&"' AND NOT M = '') OR '"&C44&"' = 'All')
ORDER BY T ASC, dateDiff(date'"&TEXT(A39,"yyyy-MM-dd")&"',G) ASC
LABEL dateDiff(date'"&TEXT(A39,"yyyy-MM-dd")&"',G) 'Days After Last Update',T 'Days Before Deadline'",1

2. Create multiple pivot tables from the queried table, depending on what information should be displayed onto the dashboard
3. Visualize the pivot tables created.
