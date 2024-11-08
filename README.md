# Assignment-1 (Data Flow Level)

module multiplier_dataflow (
    input [2:0] A,   // 3-bit operand A
    input [2:0] B,   // 3-bit operand B
    output [5:0] P   // 6-bit product output
);

    assign P = A * B;  // Multiplying A and B directly

endmodule
