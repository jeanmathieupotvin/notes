#' Entry point
#'
#' Prepare an R session for development purposes.

# Ensure that development dependencies can
# be loaded, and attach these packages to
# R's search path.
if (interactive()) {
    suppressMessages({
        require("knitr")
        require("rmarkdown")
        require("whereami")
    })
}

# Create a function that compiles RMarkdown files to their
# GFM (Github Flavored Markdown) equivalent. Options are
# standardized.
compile <- function()
{
    # Get currently active file. This is where
    # compile() should be written and called.
    active_file <- rstudioapi::documentPath()

    # Render RMarkdown document to the GFM format.
    return(
        invisible(
            rmarkdown::render(
                input         = active_file,
                output_format = rmarkdown::md_document(
                    variant         = "gfm",
                    preserve_yaml   = FALSE,
                    toc             = FALSE,
                    number_sections = FALSE),
                output_file   = file.path(dirname(active_file), "README.md"))))
}
