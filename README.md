# SwiftUI-Crud-Operation

func solveNQueens(_ n: Int) -> [[String]] {
        guard n > 0 else {
            return [[String]]()
        }
    
        var boards = [[String]]()
        var board = Array(repeating: "", count: n)
        
        depthFirstSearch(&boards, &board, n, 0)
        
        return boards
    }
    
    private func depthFirstSearch(_ boards: inout [[String]], _ board: inout [String], _ n: Int, _ row: Int) {
        if row == n {
            boards.append(Array(board))
            return
        }
        
        
        for col in 0..<n {
            if isValid(board, col, row) {
                board[row] = setRow(col, n)
                depthFirstSearch(&boards, &board, n, row + 1)
            }
        }
    }
    
    private func isValid(_ board: [String], _ col: Int, _ row: Int) -> Bool {
        var c = -1
    
        for i in 0..<row {
            for j in 0..<board[0].count {
                if charAt(board[i], j) == "Q" {
                    c = j
                    break
                }
            }
            
            // check col
            if c == col {
                return false
            }
            
            // check diagnol
            if abs(c - col) == abs(i - row) {
                return false
            }
        }
        
        return true
    }
    
    private func charAt(_ str: String, _ index: Int) -> Character {
        return str[str.index(str.startIndex, offsetBy: index)]
    }
    
    private func setRow(_ col: Int, _ n: Int) -> String {
        var row = ""
        
        for i in 0..<n {
            if i == col {
                row.append("Q")
            } else {
                row.append("0")
            }
        }
        
        return row
    }
