# Assignment-1
module multiplier_gate_level (
    input [2:0] A,   // 3-bit operand A
    input [2:0] B,   // 3-bit operand B
    output [5:0] P   // 6-bit product output
);

    wire [2:0] p0, p1, p2;   // Partial products
    wire c1, c2, c3, c4, c5, c6; // Carry wires

    // Partial products
    assign p0 = A[0] ? B : 3'b000;  // A0 * B
    assign p1 = A[1] ? B : 3'b000;  // A1 * B
    assign p2 = A[2] ? B : 3'b000;  // A2 * B

    // Sum partial products using half and full adders

    // First bit of P
    assign P[0] = p0[0];

    // Second bit of P
    half_adder ha1 (.a(p0[1]), .b(p1[0]), .sum(P[1]), .carry(c1));

    // Third bit of P
    full_adder fa1 (.a(p0[2]), .b(p1[1]), .cin(p2[0]), .sum(P[2]), .carry(c2));

    // Fourth bit of P
    full_adder fa2 (.a(p1[2]), .b(p2[1]), .cin(c1), .sum(P[3]), .carry(c3));

    // Fifth bit of P
    half_adder ha2 (.a(p2[2]), .b(c2), .sum(P[4]), .carry(c4));

    // Sixth bit of P
    assign P[5] = c3 | c4;

endmodule

// Half Adder module
module half_adder (
    input a, b,
    output sum, carry
);
    assign sum = a ^ b;
    assign carry = a & b;
endmodule

// Full Adder module
module full_adder (
    input a, b, cin,
    output sum, carry
);
    assign sum = a ^ b ^ cin;
    assign carry = (a & b) | (b & cin) | (cin & a);
endmodule
