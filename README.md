# INTEGER-TO-ENGLISH-WORDS
class Solution(object):
    def numberToWords(self, num):
        if num == 0:
            return "Zero"

        below20 = ["", "One", "Two", "Three", "Four", "Five", "Six", "Seven",
                   "Eight", "Nine", "Ten", "Eleven", "Twelve", "Thirteen",
                   "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen",
                   "Nineteen"]
        tens = ["", "", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy",
                "Eighty", "Ninety"]
        thousands = ["", "Thousand", "Million", "Billion"]

        def helper(n):
            """Convert a number < 1000 to words (no trailing spaces trimmed here)."""
            if n == 0:
                return ""
            if n < 20:
                return below20[n] + " "
            if n < 100:
                return tens[n // 10] + " " + helper(n % 10)
            return below20[n // 100] + " Hundred " + helper(n % 100)

        res = ""
        i = 0
        while num > 0:
            chunk = num % 1000
            if chunk != 0:
                res = helper(chunk) + (thousands[i] + " " if thousands[i] else "") + res
            num //= 1000
            i += 1

        return res.strip()
