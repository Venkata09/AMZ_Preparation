# Reorganize String 

```java

public String reorganizeString(String inputString) {
        String outputString = "";

        int[] charArray = new int[26];
        /* For finding the count of each element. */
        for (int i = 0; i < inputString.length(); i++) {
            charArray[inputString.charAt(i) - 'a'] += 1;
        }


        Comparator<int[]> comp = new Comparator<int[]>() {
            public int compare(int[] a1, int[] a2) {
                return a2[0] - a1[0];
            }
        };
        /* So now the head is sorted. */
        PriorityQueue<int[]> heap = new PriorityQueue<>(comp);

        /* What is the purpose of this LIMIT ?? */
        int limit = (inputString.length() + 1) / 2;

        for (int i = 0; i < charArray.length; i++) {
            /* It will give each character count. */
            int eachCharCount = charArray[i];
            if (eachCharCount > limit) {
                return "";
            }

            if (eachCharCount > 0)
                heap.add(new int[]{eachCharCount, 'a' + i});


        }


        StringBuilder sb = new StringBuilder();
        while (!heap.isEmpty()) {
            int[] currentEntry = heap.poll();
            /* How this condition will get the solution ?? How this condition helps*/
            if (sb.length() == 0 || sb.charAt(sb.length() - 1) != (char) currentEntry[1]) {
                sb.append((char) currentEntry[1]);
                if (currentEntry[0] > 1) {
                    currentEntry[0] -= 1;
                    heap.add(currentEntry);
                }
            }
            //if most frequent one has been used previously - use next one from the min heap
            else {
                int[] p = heap.poll();
                sb.append((char) p[1]);
                if (p[0] > 1) {
                    p[0] -= 1;
                    heap.add(p);
                }
                //put back most frequent one for next iterations
                heap.add(currentEntry);
            }
        }

        return sb.toString();
    }
    
    
```    
