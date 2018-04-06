# Introduction

```kotlin
listOf(1,2,3).println()


fun DataFrame.unnest(columnName: String = "data"): DataFrame {
    val dataCol = get(columnName).asType<DataFrame>()

    val replicationIndex = dataCol
        .mapIndexed { rowNumber, dataFrame -> IntArray(dataFrame?.nrow ?: 1, { rowNumber }) }
        .flatMap { it.toList() }



    val left = replicateByIndex(remove(columnName), replicationIndex)

    val unnested = dataCol.toList()
        .map { it ?: emptyDataFrame() }
        .bindRows()

    return bindCols(left, unnested)

}

```


GitBook integrates perfectly with GitHub as a hosting solution for the source of your book. When configured correctly, this has several effects:

All updates made to your book from the Editor will also update the GitHub repository.
All updates made to your GitBook or GitHub repository will be reflected on the other and update your published book accordingly.
Integrating with GitHub is done in 3 steps:

Setting up our GitHub Integration
Granting access to your repositories
Linking a book to a GitHub repository
Linking an existing book
Creating a new book from a GitHub repository
