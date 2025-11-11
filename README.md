# Sorting-Aglorithm-Task

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Bubble Sort Program</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #d1fae5, #a7f3d0);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-start;
            min-height: 100vh;
            margin: 0;
            padding-top: 40px;
        }

        h2 {
            color: #065f46;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.1);
            margin-bottom: 20px;
        }

        form {
            background: white;
            padding: 25px 35px;
            border-radius: 16px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
            width: 360px;
        }

        label {
            font-weight: 600;
            color: #064e3b;
        }

        input, select, button {
            width: 100%;
            margin: 8px 0 16px;
            padding: 10px 12px;
            font-size: 16px;
            border-radius: 8px;
            border: 1px solid #10b981;
            outline: none;
            transition: 0.3s;
        }

        input:focus, select:focus {
            border-color: #047857;
            box-shadow: 0 0 6px rgba(5,150,105,0.4);
        }

        button {
            background: #10b981;
            color: white;
            border: none;
            font-weight: 600;
            cursor: pointer;
            transition: 0.3s;
        }

        button:hover {
            background: #059669;
        }

        .result {
            margin-top: 25px;
            background: #ecfdf5;
            padding: 20px 25px;
            border-radius: 16px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
            width: 360px;
            color: #064e3b;
        }

        strong {
            color: #065f46;
        }

        .footer {
            margin-top: 40px;
            color: #065f46;
            font-size: 14px;
            opacity: 0.8;
        }
    </style>
</head>
<body>

  
<h2> 💚  Bubble Sort 💚  </h2>

<form method="post">
    <label>Enter numbers (comma-separated):</label>
    <input type="text" name="numbers" placeholder="e.g. 9, 2, 7, 4, 3" required>

    <label>Choose order:</label>
    <select name="order" required>
        <option value="asc">Ascending</option>
        <option value="desc">Descending</option>
    </select>

    <button type="submit">Sort Now</button>
</form>

<?php

function bubbleSort($arr, $order) {
    $n = count($arr);
    $swaps = 0;

    for ($i = 0; $i < $n - 1; $i++) {
        for ($j = 0; $j < $n - $i - 1; $j++) {
            $condition = ($order == "asc") 
                ? ($arr[$j] > $arr[$j + 1]) 
                : ($arr[$j] < $arr[$j + 1]);

            if ($condition) {
                $temp = $arr[$j];
                $arr[$j] = $arr[$j + 1];
                $arr[$j + 1] = $temp;
                $swaps++;
            }
        }
    }

    return ["sorted" => $arr, "swaps" => $swaps];
}

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $numbersInput = $_POST['numbers'];
    $order = $_POST['order'];

    $numbers = array_map('intval', explode(',', $numbersInput));
    $original = $numbers;

    $result = bubbleSort($numbers, $order);
    $sorted = $result['sorted'];
    $swaps = $result['swaps'];

    echo "<div class='result'>";
    echo "<strong>Original Array:</strong> [" . implode(", ", $original) . "]<br><br>";
    echo "<strong>Sorted (" . htmlspecialchars($order) . "):</strong> [" . implode(", ", $sorted) . "]<br><br>";
    echo "<strong>Total Swaps:</strong> $swaps";
    echo "</div>";
}
?>

<div class="footer">
    Designed with 💚 
</div>

</body>
</html>
