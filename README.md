# leetcodePROBLEM 6
Problem ; 
* "PAYPALISHIRING" dizesi, aşağıdaki gibi belirli sayıda satıra zikzak biçiminde yazılır:
 * (daha iyi okunabilirlik için bu kalıbı sabit yazı tipinde görüntülemek isteyebilirsiniz)
 *
* P   A   H   N
 * A P L S I I G
 * Y   I   R
 * Ve sonra satır satır okuyun: "PAHNAPLSIIGYIR"
 * Bir dize alacak kodu yazın ve bir dizi satır verilen bu dönüşümü yapın:
 * string convert (dize metni, int nRows);
 * convert ("PAYPALISHIRING", 3) "PAHNAPLSIIGYIR" döndürmelidir.
 Kod ;
/**
 * @param {string} s
 * @param {number} numRows
 * @return {string}
 */
var convert = function (s, numRows) {
    var arr = [];
    for (var i = 0; i < numRows; i++) {
        arr[i] = [];
    }
    var cnt = 0;
    var len = s.length;
    while (cnt < len) {
        for (var i = 0; i < arr.length && cnt < len; i++) {            arr[i].push(s[cnt++]);
        }
        for (var i = numRows - 2; i >= 1 && cnt < len; i--) {            arr[i].push(s[cnt++]);
        }
    }   
    return arr.map(arr => arr.join('')).join('')
};
console.log(convert('PAYPALISHIRING', 3));
PROBLEM 16
Problem ;
* N tamsayı dizisi S verildiğinde, toplamda belirli bir sayıya, hedefe en yakın olacak şekilde S'de üç tamsayı bulun.
* Üç tam sayının toplamını döndürün. Her bir girişin tam olarak bir çözümü olacağını varsayabilirsiniz.
 * Örneğin, verilen dizi S = {-1 2 1 -4} ve hedef = 1.
 * Hedefe en yakın olan toplam 2'dir. (-1 + 2 + 1 = 2).
Çözüm ;
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var threeSumClosest = function (nums, target) {

    var ans = nums[0] + nums[1] + nums[2];
    var len = nums.length;

    nums.sort((a, b) => a < b ? -1 : (a > b) ? 1 : 0);

    for (var i = 0; i < len - 2; i++) {
        var j = i + 1;
        var k = len - 1;

        while (j < k) {
            var sum = nums[i] + nums[j] + nums[k];
            if (sum === target) return sum;
            if (sum > target) k--;
            if (sum < target) j++;
            if (Math.abs(target - sum) < Math.abs(target - ans)) {
                ans = sum;
            }
        }
    }
    return ans;

};

console.log(threeSumClosest([-1, 2, 1, -4], 1));
PROBLEM 26
Problem ; 
* Sıralı bir dizi verildiğinde, her öğenin yalnızca bir kez görünmesi ve yeni uzunluğu döndürmesi için kopyaları kaldırın.
 * Başka bir dizi için ekstra alan ayırmayın, bunu sabit bellekle yerine yapmalısınız.
 *
 * Örneğin,
 * Verilen girdi dizisi sayısı = [1,1,2],
 * İşlevin, sayıların ilk iki öğesi sırasıyla 1 ve 2 olacak şekilde uzunluk = 2 döndürmelidir.
 * Yeni uzunluğun ötesinde ne bıraktığınız önemli değil.
Çözüm ;
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function (nums) {
    var n = nums.length;
    if (!n)  return 0;
    var last = nums[0];
    var cnt = 1;

    for (var i = 1; i < nums.length; i++) {
        if (nums[i] !== last) {
            last = nums[i];
            cnt++;
        }
        else {
            nums.splice(i, 1);
            i--;
        }
    }
    return cnt;
};

/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function (nums) {
    for (var i = 0; i < nums.length - 1; i++)
        if (nums[i] === nums[i + 1]) nums.splice(i--, 1);
    return nums.length;
};

var arr = [1, 2, 2];
console.log(removeDuplicates(arr));
console.log(arr);
PROBLEM 36
Problem ; 
* Sudoku'nun geçerli olup olmadığını belirleyin: Sudoku Bulmacaları - Kurallar.
 * Sudoku panosu, boş hücrelerin '.' Karakteriyle dolu olduğu kısmen doldurulabilir.
 * Kısmen doldurulmuş sudoku geçerlidir.
 * Not:
* Geçerli bir Sudoku kartı (kısmen doldurulmuş) mutlaka çözülemez. Yalnızca doldurulmuş hücrelerin doğrulanması gerekir.
Çözüm ;
/**
 * @param {character[][]} board
 * @return {boolean}
 */
var isValidSudoku = function (board) {
    for (var i = 0; i < 9; i++) {
        var rowNums = [];
        var colNums = [];
        var cubeNums = [];

        for (var j = 0; j < 9; j++) {
            var ch = board[i][j];
            if (ch !== '.') {
                if (rowNums.indexOf(ch) > -1) return false;
                rowNums.push(ch);
            }

            ch = board[j][i];
            if (ch !== '.') {
                if (colNums.indexOf(ch) > -1) return false;
                colNums.push(ch);
            }

            var row = Math.floor(i / 3) * 3 + Math.floor(j / 3);
            var col = i % 3 * 3 + j % 3;
            // console.log(i, j, row, col);
            ch = board[row][col];
            if (ch !== '.') {
                if (cubeNums.indexOf(ch) > -1) return false;
                cubeNums.push(ch);
            }
        }
    }
    return true;
};
console.log(isValidSudoku([
    [".", ".", "4", ".", ".", ".", "6", "3", "."],
    [".", ".", ".", ".", ".", ".", ".", ".", "."],
    ["5", ".", ".", ".", ".", ".", ".", "9", "."],
    [".", ".", ".", "5", "6", ".", ".", ".", "."],
    ["4", ".", "3", ".", ".", ".", ".", ".", "1"],
    [".", ".", ".", "7", ".", ".", ".", ".", "."],
    [".", ".", ".", "5", ".", ".", ".", ".", "."],
    [".", ".", ".", ".", ".", ".", ".", ".", "."],
    [".", ".", ".", ".", ".", ".", ".", ".", "."]]))



PROBLEM 46
Problem ;
* Farklı sayılardan oluşan bir koleksiyon göz önüne alındığında, olası tüm permütasyonları döndürün.
 * Örneğin,
 * [1,2,3] aşağıdaki permütasyonlara sahiptir:
 * [
 * [1,2,3],
 * [1,3,2],
 * [2,1,3],
 * [2,3,1],
 * [3,1,2],
 * [3,2,1]
 *]
Çözüm ;
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var permute = function (nums) {
    if (!nums.length) return [];
    var res = [[]];
    for (var i = 0; i < nums.length; i++) {
        var len = res.length;
        for (var j = 0; j < len; j++) {
            var oldArr = res.shift();
            for (var k = 0; k <= oldArr.length; k++) {
                var newArr = oldArr.slice();
                newArr.splice(k, 0, nums[i]);
                res.push(newArr);
            }
        }
    }
    return res;
};
console.log(permute([1, 2, 3]));

PROBLEM 226

Problem;
* Bir ikili ağacı ters çevirin.
*        4
 *       / \
 *    2    7
 *   / \     / \
 * 1  3  6  9
 *
 * -
 *
 *        4
 *        / \
 *     7    2
 *   / \     / \
 * 9  6  3  1
* İkili ağaç düğümü tanımı.
* function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }


Çözüm;
/**
 * @param {TreeNode} root
 * @return {TreeNode}
 */
var invertTree = function (root) {
    if (!root) return root;
    if (!root.left && !root.right) return root;
    var left = invertTree(root.right);
    var right = invertTree(root.left);
    root.left = left;
    root.right = right;
    return root;
};

console.log(invertTree({
    val: 4,
    left: {
        val: 2,
        left: {
            val: 1,
            left: null,
            right: null,
        },
        right: null
    },
    right: null
}));





