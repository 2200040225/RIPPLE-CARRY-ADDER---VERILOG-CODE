Design code:

//HALF ADDER

module HA(
input a,b,
output s,c
);
assign s=a^b;
assign c=a&b;
endmodule

//FULL ADDER

module FA(
input a,b,cin,
output s,c);
HA1 HA(a,b,w1,w2);
HA2 HA(w1,cin,s,w3);
endmodule

//RIPPLCE CARRY ADDER

module RCA(
input [3:0]a,b;
input cin;
output [3:0]s;
output c;
wire c1,c2,c3;
FA0 FA(a[0],b[0],cin,s[0],c1);
FA1 FA(a[1],b[1],c1,s[1],c2);
FA2 FA(a[2],b[2],c2,s[2],c3);
FA3 FA(a[3],b[3],c3,s[3],c);
endmodule

Test bench:

module RCA_tb();
reg [3:0]a,b;
reg cin;
wire [3:0]s;
wire c;
RCA uut(a,b,cin,s,c);
inital begin
a=0;b=1;cin=1;
#10
a=1;b=1;cin=1;
#10
a=1;b=1;cin=0;
#10
a=0;b=0;cin=1;
#10
end
$finish();
endmodule
