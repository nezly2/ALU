# ALU
Crear una ALU con verilog

//Practica 1: ALU
Enero 22, 2021

module Practica1(
	input [3:0] iA,
	input [3:0] iB,
	input [3:0] opCode,
	output [4:0] status, //flag
	output [3:0] result 
	);

reg [4:0] resultado; //De 5 bits para poder contar el carry
assign result = resultado;
reg [4:0] flag;
assign status = flag;

always @*
 begin
 
 if((resultado[2:0] <= 3'b111)&&(flag[2] == 1))//Overflow Flag
	begin
		flag[0]=1;
	end
 else
	begin
		flag[0]=0;
	end

 if(resultado[3] == 1)//Sign Flag
	begin
		flag[1]=1;
	end
 else
	begin
		flag[1]=0;
	end

 if((resultado[4] == 1))//Carry Flag  
	begin 
		flag[2]=1;
	end
 else
	begin
		flag[2]=0;
   end
 
 
 if(resultado[3:0] == 0)//Zero Flag
	begin
		flag[3]=1;
	end
 else
	begin
		flag[3]=0;
	end
 
 
 if(resultado[3] ^ resultado[2] ^ resultado[1] ^  resultado[0])//Parity Flag
	begin
		flag[4]=1;
	end
 else 
	begin
		flag[4]=0; 
	end
	
	case(opCode)
		
		4'b0001: resultado = (iA + iB); 			 //0001:Suma
		4'b0010: resultado = (iA - iB); 			 //0010:Resta
		4'b0011: resultado = (iA & iB);			         //0011:And
		4'b0100: resultado = (iA | iB);		  	        //0100:Or
		4'b0101: resultado = ~(iA); 			            //0101:Not
		4'b0110: resultado = (iA ^ iB); 			 //0110:Xor
		4'b0111: resultado = ~iA;				       //0111:Complemento a 1
		4'b1000: resultado = ((~iA)+1); 			 //1000:Complemento a 2
		4'b1001: resultado = iA << 1;			     //1001:Shift aritmético izquierda
		4'b1010: resultado = {iA[3],iA[3:1]};	 //1010:Shift aritmético derecha 
		4'b1011: resultado = iA << 1;			     //1011:Shift lógico izquierda
		4'b1100: resultado = iA >> 1;		    	 //1100:Shift lógico derecha
		4'b1101: resultado = {iA[2:0],iA[3]};	 //1101:Rotación izquierda
		4'b1110: resultado = {iA[0],iA[3:1]};	 //1110:Rotación derecha
	endcase
 end 
endmodule

