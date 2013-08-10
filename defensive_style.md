# Defensive Programming
.fx: quote

A form of defensive design intended to ensure the continuing function of a
piece of software in spite of unforeseeable usage of said software.

Defensive programming techniques are used especially when a piece of software
could be misused mischievously or inadvertently to catastrophic effect.

[Defensive Programming](http://en.wikipedia.org/wiki/Defensive_programming)

--------------------------------------------------

# Guidelines

- Every line of code is a liability
- Codify your assumptions
- Executable documentation is preferable

--------------------------------------------------

# Python tools

- Asserts
- Logging
- Unit tests

--------------------------------------------------

# Example

    !python
    def normalize_ranges(original_data_range):
        colspan = button_state['datamax'] - button_state['datamin']

        # 1-D numpy array of data
        live_data = get_column_data(button_state['colname'])

        ratio = {}
        ratio['min'] = button_state['datamin'] / colspan
        ratio['max'] = button_state['datamax'] / colspan

        return ratio
